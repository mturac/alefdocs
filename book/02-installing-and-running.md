# 2. Installing And Running Alef

You do not need the private Alef source repository. Public usage starts with a
binary named `alef`.

## Install On macOS Apple Silicon

Download the current public binary:

```bash
curl -L -o alef \
  https://github.com/mturac/aleflang-docs/releases/latest/download/alef-darwin-arm64
chmod +x ./alef
./alef --version
```

Expected output starts with:

```text
Alef VM v1.0.0-rc.1
```

Move it onto your `PATH`:

```bash
mkdir -p ~/.local/bin
mv ./alef ~/.local/bin/alef
```

Open a new terminal or make sure `~/.local/bin` is on your `PATH`, then check:

```bash
alef --version
```

## Create Your First File

Make a folder for learning:

```bash
mkdir alef-learning
cd alef-learning
```

Create `main.alef`:

```alef
fn main() {
    println("hello, Alef")
}
```

Run it:

```bash
alef run main.alef
```

Expected output:

```text
hello, Alef
```

## Useful Commands

```bash
alef help
alef version
alef run main.alef
alef repl
alef test
```

The shorter form also works:

```bash
alef main.alef
```

This book uses `alef run main.alef` because it is explicit.

## When Something Fails

If the command is not found, your terminal cannot find the binary:

```text
command not found: alef
```

Fix it by running the binary directly:

```bash
./alef --version
```

or by moving it onto your `PATH`.

If the file is missing, check the current folder:

```bash
ls
```

You should see `main.alef`.

## Public Examples Without Source Access

Public example repositories should contain `.alef` programs, fixtures, smoke
scripts, and README instructions. They should not require access to the private
Alef compiler or runtime source tree.

Example repos should accept `ALEF_BIN`:

```bash
ALEF_BIN=/path/to/alef bash scripts/smoke.sh
```

If `ALEF_BIN` is not set, examples should fall back to `alef` from `PATH`.

## macOS: sign the binary

After downloading and placing the `alef` binary, ad-hoc sign it so macOS
Taskgated does not block execution:

```bash
chmod +x ./alef
codesign --force -s - ./alef
./alef --version
```

Public docs: [What's New — July 2026](../docs/reference/whats-new-2026-07.md).
