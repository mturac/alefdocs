# 9. The Alef CLI And Native Runtime

The main command is:

```bash
alef run main.alef
```

This runs the program on the native runtime.

## Diagnostics

```bash
alef health
alef doctor
```

Use these commands when the runtime or environment does not behave as expected.

## Tests

```bash
alef test .
```

## Bytecode

```bash
alef --bytecode run main.alef
alef --strict-bytecode run main.alef
```

Use strict bytecode mode when testing bytecode support. Use normal `alef run`
for public examples unless the page is specifically about bytecode.
