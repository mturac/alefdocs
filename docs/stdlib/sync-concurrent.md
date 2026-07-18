# Sync And Concurrent Reference

Native path. Mutex-style coordination and join helpers for promises.

## `std.sync` (mutex subset)

| Function | Role |
|----------|------|
| `mutex()` | Create a mutex handle |
| `lock(m)` / `unlock(m)` | Acquire / release |
| `try_lock(m)` | Non-blocking lock attempt |
| `rwmutex()` | Reader/writer mutex |
| `read_lock` / `read_unlock` | Shared read access |
| `write_lock` / `write_unlock` | Exclusive write access |

```alef
import std.sync { mutex, lock, unlock }

fn main() {
    let m = mutex()
    lock(m)
    // critical section
    unlock(m)
    println("ok")
}
```

More primitives (wait groups, once, maps, pools, barriers, semaphores) exist on
the native binary; document the call you use after verifying with `alef run`.

## `std.concurrent`

| Function | Role |
|----------|------|
| `when_all(items)` | Await every promise in an array; plain values pass through |
| `when_any(items)` | First settled racer (promise race); empty array errors |
| `race(items)` | Alias of `when_any` |

```alef
import std.concurrent { when_all, when_any }

fn main() {
    // Plain values: when_all returns them in order.
    let all = when_all(["a", "b", "c"])
    println(all)

    // when_any returns the first settled item (promises or values).
    let first = when_any(["ready"])
    println(first)
}
```

### When to use which

| Need | Prefer |
|------|--------|
| Collect every async result | `when_all` |
| First completed worker | `when_any` / `race` |
| Shared mutable state | `std.sync` mutexes |

## Related

- [Time And IO](time-io.md) for sleep/monotonic clocks while waiting
- [Jobs](jobs.md) for background work queues
