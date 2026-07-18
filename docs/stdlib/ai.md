# AI Providers

Alef treats AI provider calls as a standard-library surface.

## Deterministic Stub

Use `stub` in docs and tests:

```alef
fn main() {
    let r = std.ai.response_with("stub", "Summarize this ticket")
    println(r.provider)
    println(r.text)
}
```

The stub provider makes examples runnable without credentials.

## Configured Provider

```alef
let r = std.ai.response("Summarize this ticket")
```

Use environment variables to configure live providers.

## Named Providers

```alef
let r = std.ai.response_with("ollama", "hello")
let r = std.ai.response_with("minimax", "hello")
let r = std.ai.response_with("mimo", "hello")
```

Provider availability is environment-gated. A skipped live provider check is
not a failure unless the task explicitly requires that provider.

## `call_llm` and `stream_llm`

In addition to `response` and `response_with`, Alef supports lower-level interactions:

```alef
// Single call
let result = std.ai.call_llm("ollama", "Summarize this ticket");
println(result);

// Streaming call
std.ai.stream_llm("ollama", "Write a long story", fn(chunk) {
    println("Received chunk: " + chunk);
});
```

## `embed`

Alef provides an `embed` function to generate embeddings from text.

```alef
let embedding = std.ai.embed("ollama", "Hello world");
println(embedding[0]); // First float in the embedding vector
```

## Chat helpers

Higher-level chat APIs accept message lists (role + content). Prefer them for
multi-turn agents:

```alef
let r = std.ai.chat_with("stub", [
    { "role" => "system", "content" => "You are a concise assistant." },
    { "role" => "user", "content" => "Summarize: deploy failed on auth" }
])
println(r.text)
```

Streaming variants exist for token/chunk delivery (`stream`, `chat_stream`, and
`*_with` / `*_options` forms depending on release). Always keep a `stub` path
for docs and tests.

## Tool-calling (advanced)

Some providers support tool/function calls via `chat_with_tools` style APIs.
Treat tool schemas as application data (maps/JSON), not as a separate language
feature. Gate live providers with environment checks.

## Pairing AI with HTTP and jobs

A common production shape is:

1. `std.http` serves `/api/chat`, `/api/history`, health, and shutdown.
2. `std.ai` answers prompts (stub in CI, real provider in prod).
3. `std.db` stores sessions.
4. `std.jobs` runs background work with retry.

See [What's New — July 2026](../reference/whats-new-2026-07.md) and the
[AI workflow tutorial](../tutorials/ai-workflow.md).
