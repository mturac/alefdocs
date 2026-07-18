# CLI Reference

## Run

```bash
alef run main.alef
```

Runs with the native runtime by default.

## Interpreter Path

```bash
alef run --interp main.alef
```

Use this for development surfaces that are not native-first.

## Build

```bash
alef build main.alef
```

Builds through the optional Go codegen path.

## Diagnostics

```bash
alef health
alef doctor
```

## Test

```bash
alef test .
```

Use `@test` functions for test discovery.
