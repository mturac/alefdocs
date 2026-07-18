# Cookbook: Provider-gated AI Calls

Use the stub provider for tests:

```alef
let r = std.ai.response_with("stub", "hello")
```

Use a named provider when the environment is configured:

```alef
let r = std.ai.response_with("ollama", "hello")
```

Use the default provider for deployed environments:

```alef
let r = std.ai.response("hello")
```

Smoke scripts should treat optional live providers as gated:

```bash
if [[ -z "${ALEF_OPENAI_API_KEY:-}" ]]; then
  echo "OPENAI_KEY_MISSING: skipped optional live smoke"
  exit 0
fi
```

Do not hardcode credentials in docs or examples.
