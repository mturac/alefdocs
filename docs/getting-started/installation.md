# Installation

Alef's source repository is private. Public users install or receive the `alef`
command and write `.alef` programs against the documented language contract.

## Install The Command

Use the release channel provided by the Alef team. The current public build is
for macOS arm64:

```bash
curl -L -o alef \
  https://github.com/mturac/aleflang-docs/releases/latest/download/alef-darwin-arm64
chmod +x ./alef
./alef --version
```

Move it onto your `PATH` when you are ready:

```bash
mkdir -p ~/.local/bin
mv ./alef ~/.local/bin/alef
alef --version
```

If you are given a standalone binary, make it executable and run it directly:

```bash
chmod +x ./alef
./alef --version
```

Then run a program:

```bash
alef run main.alef
```

## Requirements

- an `alef` command or standalone Alef binary
- Node.js only for JavaScript-based example tooling
- Go only when a public example uses the optional Go codegen path

You do not need the private compiler or runtime source tree to follow this
documentation.

## Available Public Build

- `alef-darwin-arm64`: macOS Apple Silicon

Additional platform binaries can be attached to the same GitHub release without
opening the Alef source repository.

## Recommended Example Hook

Public example repositories should accept `ALEF_BIN`:

```bash
ALEF_BIN=/path/to/alef bash scripts/smoke.sh
```

If `ALEF_BIN` is not set, examples should fall back to `alef` from `PATH`.
