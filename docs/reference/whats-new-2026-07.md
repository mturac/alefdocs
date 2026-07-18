# What's New — July 2026

This page summarizes documentation-facing language and runtime updates as of
**2026-07-18**. It is written for people learning and shipping with the public
`alef` binary. Compiler source remains private; public docs live in this repo
([alefdocs](https://github.com/mturac/alefdocs)).

## Docs home moved to AlefDocs

| Before | After |
|--------|--------|
| Docs mixed with the private language repo | Public site: **https://mturac.github.io/alefdocs/** |
| Pages blocked on private billing limits | Public repo deploys GitHub Pages from `main` |

You only need this site and a release binary — not a private source checkout.

## Native-first is the default path

Public examples and tutorials target:

```bash
alef run main.alef
```

That path uses the native runtime. Prefer it over any interpreter-only flags
unless a tutorial says otherwise.

### macOS install note

After you copy a release `alef` binary into place on macOS, ad-hoc sign it so
Taskgated does not block execution:

```bash
codesign --force -s - ./alef
./alef --version
```

## AI, HTTP, and data in one program

Alef's wedge for agent backends is: **one language, one binary**, with HTTP,
SQLite, jobs, and model calls as stdlib surfaces.

### Chat and streaming

```alef
// Deterministic docs/tests
let r = std.ai.chat_with("stub", [
    { "role" => "user", "content" => "Reply with: ok" }
])
println(r.text)

// Streaming completion (provider-gated when not stub)
std.ai.stream("stub", "Say hello in three words", fn(chunk) {
    println(chunk)
})
```

### HTTP + sessions + JSON

You can serve chat, history, and health endpoints from a single process:

```alef
import std.http { json_response, app, route, listen_options }

fn health(request, state) {
    return {
        "response" => json_response(json_encode({ "ok" => true })),
        "state" => state
    }
}

fn main() {
    let a = std.http.with_state(app(), {})
    a = route(a, "GET", "/health", health)
    listen_options("127.0.0.1:8090", a, {
        "shutdown_path" => "/__shutdown"
    })
}
```

### Background jobs

In-process job queues support enqueue, drain, retry/dead-letter, and optional
SQLite persist/restore across restarts (when wired in your app):

```alef
import std.jobs { make, enqueue, drain, mark_processed, mark_failed, stats }

fn main() {
    let q = make()
    enqueue(q, { "kind" => "ping" })
    let batch = drain(q, 4)
    for job in batch {
        if job != null {
            mark_processed(q, true)
        }
    }
    println(stats(q))
}
```

Use the [AI workflow tutorial](../tutorials/ai-workflow.md) and
[provider-gated AI cookbook](../cookbook/provider-gated-ai.md) for full patterns.

## Standard library depth (native)

These surfaces are available on the native path used by `alef run`:

| Module | What landed |
|--------|-------------|
| `std.crypto` | Random bytes, digests, HMAC-SHA256, common primitives (AES, Ed25519, PBKDF2, and more) |
| `std.encoding` | Base64 encode/decode helpers |
| `std.http` | Cookie parse/format helpers, richer client/server options, templates/TLS-related work |
| `std.concurrent` | `when_all` / `when_any` style helpers |
| `std.sync` / atomics | Mutexes, once, maps, pools, barriers, semaphores (native) |
| `std.time` | Sleep, parse, monotonic clock, ticker |
| `std.io` | Copy, read-all, limit, pipe, multi, tee, seek helpers |
| `std.db` | SQLite migrations, query/exec, transactions |
| `std.ai` | Completions, chat, stream, tools, embeddings (provider-gated) |
| `std.jobs` | Queue, retry, dead-letter, persist/restore hooks |

Exact function names are listed under [Standard Library Overview](../stdlib/overview.md)
and the module references.

## Maturity posture (honest)

Alef is **AI-native + native-first**. It is **not** claiming full Go or .NET
stdlib parity.

What that means for you:

- Ship with the **documented stdlib surfaces** and the public tutorials.
- Treat Go/.NET-class breadth as a long multi-year journey, not a weekly checklist.
- Internal inventory scaffolding is **not** a public completion metric and is
  not tracked on this site.

## Documentation site

| Resource | URL |
|----------|-----|
| Live docs | https://mturac.github.io/alefdocs/ |
| Docs source | https://github.com/mturac/alefdocs |
| Language repo | private (`mturac/aleflang`) |

## Related pages

- [Release Notes](release-notes.md) — chronological doc-facing notes
- [AI Reference](../stdlib/ai.md)
- [HTTP And JSON](../stdlib/http-json.md)
- [Installing And Running](../../book/02-installing-and-running.md)
