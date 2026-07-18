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
