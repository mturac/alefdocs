# Standard Library Overview

Alef is a programming language, and the standard library is part of that
language experience. Surfaces below are available on the **native** path used
by `alef run` unless a page says otherwise.

## Core surfaces

| Module | Role |
|--------|------|
| `std.http` | Clients, JSON/problem responses, app router, middleware, cookies, limits, metrics, shutdown |
| `std.json` / `json_encode` / `json_decode` | Structured data |
| `std.ai` | Completions, chat, streaming, tools, embeddings (provider-gated; `stub` for docs) |
| `std.db` | SQLite migrations, query, exec, transactions |
| `std.cache` | Small stateful helpers |
| `std.jobs` | In-process queues, retry/dead-letter, optional persist/restore |
| `std.crypto` | Random, digests, HMAC, common crypto primitives |
| `std.encoding` | Base64 and related helpers |
| `std.concurrent` | Join helpers such as `when_all` / `when_any` |
| `std.sync` | Synchronization primitives (mutex/once/map/pool class) |
| `std.time` | Sleep, parse, monotonic clocks, tickers |
| `std.io` | Stream copy/limit/pipe helpers |
| `std.view` / `std.http.html` | Server-rendered HTML examples |
| `std.workflow` / `std.goal` | Durable work sketches (see runtime examples) |

## How to read this

1. Prefer **module references** and book chapters over guessing package names.
2. Live AI providers need env configuration; use **`stub`** in tutorials and CI.
3. July 2026 capability summary: [What's New — July 2026](../reference/whats-new-2026-07.md).

The stdlib is documented like a language stdlib: module by module, with
runnable examples.
