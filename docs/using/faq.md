# Frequently Asked Questions

## Is Alef a programming language?

Yes. Alef has its own syntax, runtime, command-line tool, modules, standard
library, and examples. It can be used to build apps, but it is not merely an app
template or framework.

## Is `alef run` the production path?

Yes. Public docs and examples should target the native runtime through:

```bash
alef run main.alef
```

## When should I use `--interp`?

Use `alef run --interp` for interpreter/dev surfaces that are not native-first.
Do not make it the default in production examples.

## When should I use maps instead of structs?

Use maps for JSON-heavy request, response, and UI state. Use structs when a
domain shape deserves a stable name and stronger documentation.

## Does Alef require AI credentials?

No. Docs and smoke tests should use the deterministic `stub` provider. Live
providers are optional and environment-gated.

## Why are there UI and ticket examples in language docs?

Because examples should show real programs. They demonstrate the language and
standard library in use; they do not define Alef as a framework.
