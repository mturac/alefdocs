# Cookbook: AI Agent Backend

Build a small agent backend as **one native process**: HTTP API + AI + optional
SQLite sessions + background jobs.

## Shape

1. Listen with `std.http.listen_options` and a shutdown path for tests.
2. Route `POST /api/chat` to a handler that calls `std.ai.chat_with` or `stream`.
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

## Tips

- Keep `stub` available for CI and local docs runs.
- Gate live providers with environment variables.
- Prefer explicit JSON request/response maps over hidden frameworks.
- See [What's New — July 2026](../reference/whats-new-2026-07.md).
