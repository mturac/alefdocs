# Cookbook: AI Agent Backend

Build a small agent backend as **one native process**: HTTP API + AI + optional
SQLite sessions + background jobs.

## Shape

1. Listen with `std.http.listen_options` and a shutdown path for tests.
2. Route `POST /api/chat` to a handler that calls `std.ai.chat_with` (stub-safe).
3. Store turns in `std.db` when you need history across restarts.
4. Enqueue side work with `std.jobs` (audit, webhooks, retries).

## Minimal chat handler (stub-safe)

```alef
import std.http { json_response, problem_response }

fn with_state(response, state) {
    return { "response" => response, "state" => state }
}

fn chat(request, state) {
    let body = json_decode(request["body"])
    let prompt = body["prompt"]
    if prompt == null or prompt == "" {
        return with_state(problem_response(400, "bad_request", "missing prompt", "req-1"), state)
    }
    let r = std.ai.chat_with("stub", [
        { "role" => "user", "content" => prompt }
    ])
    return with_state(json_response(json_encode({
        "text" => r.text,
        "provider" => r.provider
    })), state)
}
```

## Multi-turn messages

Pass the full history each request. Keep roles explicit (`user` / `assistant` /
`system`):

```alef
fn chat_turns(request, state) {
    let body = json_decode(request["body"])
    let messages = body["messages"]
    if messages == null {
        return with_state(problem_response(400, "bad_request", "missing messages", "req-2"), state)
    }
    let r = std.ai.chat_with("stub", messages)
    return with_state(json_response(json_encode({
        "text" => r.text,
        "provider" => r.provider
    })), state)
}
```

Streaming variants (`stream`, `chat_stream`, and `*_with` forms) exist on the
native AI surface — always keep a **`stub`** path for CI and docs runs.

## Sessions with `std.db` (sketch)

Store turns keyed by session id. Exact SQL helpers follow [Database And Cache](../stdlib/db-cache.md):

```alef
// Pseudocode shape — wire exec/query to your migration table.
fn append_turn(db, session_id, role, content) {
    // std.db.exec(db, "INSERT INTO turns(session_id, role, content) VALUES (?, ?, ?)",
    //     [session_id, role, content])
    return true
}

fn load_turns(db, session_id) {
    // return std.db.query(db, "SELECT role, content FROM turns WHERE session_id = ? ORDER BY id",
    //     [session_id])
    return []
}
```

On `POST /api/chat`:

1. Read `session_id` + `prompt` from JSON.
2. `load_turns` → append user message → `chat_with` → append assistant text.
3. Return `{ text, session_id }`.

## Jobs for side work

After a successful chat, enqueue non-critical work so the HTTP path stays thin:

```alef
import std.jobs { make, enqueue, drain, mark_processed, stats }

fn main() {
    let q = make()
    enqueue(q, {
        "kind" => "audit",
        "session_id" => "s-1",
        "prompt_len" => 42
    })
    let batch = drain(q, 8)
    for job in batch {
        if job != null {
            // send webhook / write audit row
            mark_processed(q, true)
        }
    }
    println(stats(q))
}
```

Dead-letter path: `mark_failed(q, reason)` when processing throws or returns a
hard error. Optional `persist` / `restore` keep the queue across restarts.

## End-to-end checklist (copy-paste goal)

| Step | Surface | Done when |
|------|---------|-----------|
| 1 | `listen_options` + `/__shutdown` | Server starts and stops in tests |
| 2 | `POST /api/chat` + `stub` | Returns JSON without provider keys |
| 3 | Multi-turn `messages` | History list accepted |
| 4 | `std.db` turns table | History survives process restart |
| 5 | `std.jobs` audit enqueue | Drain loop marks processed |

## Tips

- Keep `stub` available for CI and local docs runs.
- Gate live providers with environment variables — see [Provider-Gated AI](provider-gated-ai.md).
- Prefer explicit JSON request/response maps over hidden frameworks.
- Cookie sessions: [HTTP cookies](../stdlib/http-json.md#cookies) + never store raw secrets client-side.
- Depth references: [AI](../stdlib/ai.md) · [Jobs](../stdlib/jobs.md) · [Crypto](../stdlib/crypto-encoding.md).
- Snapshot: [What's New — July 2026](../reference/whats-new-2026-07.md).
