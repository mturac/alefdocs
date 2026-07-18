# Release Notes

This page records documentation-facing release notes.

## Native-first Docs

Public examples target:

```bash
alef run main.alef
```

## HTTP Client Result Behavior

Native HTTP client calls return `Result<HttpResponse, string>`:

```alef
match std.http.get("https://example.com") {
    Ok(r) => println(r.body),
    Err(e) => println("request failed: {e}"),
}
```

## Bytecode Strict Mode

Use strict bytecode checks when validating bytecode support:

```bash
alef --strict-bytecode run main.alef
```
