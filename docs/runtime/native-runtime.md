# Native Runtime

The native runtime is the default production-facing path.

```bash
alef run main.alef
```

It supports:

- CLI execution
- HTTP server routes
- JSON encode/decode
- SQLite-backed examples
- cache helpers
- AI provider surfaces
- smoke-test friendly shutdown and metrics endpoints

## Server Options

```alef
std.http.listen_options("127.0.0.1:8097", app(), {
    "timeout_ms" => 30000,
    "max_body_bytes" => 4096,
    "metrics_path" => "/__metrics",
    "shutdown_path" => "/__shutdown"
})
```

Use `shutdown_path` in examples so smoke tests can stop the server cleanly.
