# Jobs Reference

Native path. In-process job queues with drain, retry/dead-letter hooks, and
optional persist/restore.

## `std.jobs`

| Function | Role |
|----------|------|
| `make()` | Create a queue |
| `enqueue(q, job)` | Push a job map/value |
| `dequeue(q)` | Pop one job |
| `drain(q, n)` | Take up to `n` jobs |
| `len(q)` | Queue length |
| `stats(q)` / `metrics(q)` | Counters for observability |
| `mark_processed(q, ok)` | Record success path |
| `mark_failed(q, err)` | Record failure / dead-letter path |
| `persist(q, path)` / `restore(q, path)` | Optional disk hooks |
| `schedule` / `tick` / `schedules` | Delayed work helpers |

### Minimal drain loop

```alef
import std.jobs { make, enqueue, drain, mark_processed, mark_failed, stats }

fn main() {
    let q = make()
    enqueue(q, { "kind" => "ping" })
    enqueue(q, { "kind" => "pong" })

    let batch = drain(q, 4)
    for job in batch {
        if job != null {
            // process job["kind"] here
            mark_processed(q, true)
        } else {
            mark_failed(q, "empty")
        }
    }
    println(stats(q))
}
```

```bash
alef run main.alef
```

### Persist sketch

When your app needs restart survival, call `persist` after enqueue bursts and
`restore` on boot. Paths and exact map shapes follow the binary you ship —
verify with a small local program before production.

## Agent backend pattern

1. HTTP handler enqueues side work (`audit`, `webhook`).
2. A drain loop (same process or worker tick) processes the batch.
3. Failures go through `mark_failed` so dead-letter counts stay visible.

See [AI Agent Backend](../cookbook/ai-agent-backend.md) for the end-to-end recipe.

## Related

- [AI Reference](ai.md)
- [Database And Cache](db-cache.md)
- [What's New — July 2026](../reference/whats-new-2026-07.md)
