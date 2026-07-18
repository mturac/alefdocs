# 12. AI As Standard Library

Alef is AI-native because AI provider calls are standard-library work.

## Stub Provider

Use the deterministic stub provider in docs and tests:

```alef
fn main() {
    let r = std.ai.response_with("stub", "Summarize this ticket")
    println(r.provider)
    println(r.text)
}
```

This runs without credentials.

## Named Providers

```alef
let r = std.ai.response_with("ollama", "hello")
let r = std.ai.response_with("minimax", "hello")
let r = std.ai.response_with("mimo", "hello")
```

Live provider checks should be environment-gated. Missing optional credentials
should produce a clear skip message, not a fake success.

## Why This Belongs In A Language Book

AI calls are not the whole language. They are a standard-library surface, just
like HTTP or JSON. They are documented here because modern programs use them.
