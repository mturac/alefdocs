# Time And IO Reference

Native path. Clocks, sleep, tickers, and stream helpers.

## `std.time`

| Function | Role |
|----------|------|
| `now()` | Unix epoch seconds as float |
| `sleep(ms)` | Block current thread for milliseconds |
| `parse(rfc3339)` | Parse RFC3339 → struct with `unix_secs`, `offset_secs` |
| `format(time, fmt)` | Format a time struct |
| `utc_offset_secs(rfc3339)` | Offset seconds from a timestamp string |
| `monotonic_now()` | Monotonic clock milliseconds (for durations) |
| `ticker(interval_ms)` | Create a ticker |
| `tick(t)` | Wait for next tick (count, or `-1` if stopped) |
| `ticker_stop(t)` | Stop a ticker |

### Sleep and monotonic duration

```alef
import std.time { sleep, monotonic_now }

fn main() {
    let t0 = monotonic_now()
    sleep(50)
    let t1 = monotonic_now()
    println(t1 - t0)
}
```

### Parse RFC3339

```alef
import std.time { parse }

fn main() {
    let t = parse("2026-07-18T12:00:00Z")
    println(t.unix_secs)
    println(t.offset_secs)
}
```

## `std.io`

| Function | Role |
|----------|------|
| `print` / `println` | Write to stdout |
| `read_line()` | Read one line from stdin |
| `read_file(path)` / `write_file(path, data)` | Whole-file helpers |
| `read_bytes(path)` / `read_all(reader)` | Byte/stream reads |
| `copy(...)` | Copy between stream-like handles |
| `pipe()` / pipe reader-writer helpers | In-process pipes |
| `limit(reader, n)` / `limit_reader*` | Cap how many bytes are read |

Start with file helpers for scripts; use pipe/limit when composing streams.

```alef
import std.io { write_file, read_file }

fn main() {
    write_file("/tmp/alef-io-demo.txt", "hello")
    println(read_file("/tmp/alef-io-demo.txt"))
}
```

## Notes

- Prefer `monotonic_now` for elapsed time; prefer `now` for wall-clock stamps.
- File paths are process-local; do not hardcode secrets into files you commit.

## Related

- [Crypto And Encoding](crypto-encoding.md)
- [HTTP And JSON](http-json.md)
