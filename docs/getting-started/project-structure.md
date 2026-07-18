# Project Structure

A small Alef project can stay very small:

```text
my-alef-app/
├── alef.mod
├── main.alef
├── README.md
└── scripts/
    └── smoke.sh
```

## `alef.mod`

```text
module my-alef-app

version 0.1.0
```

## `main.alef`

```alef
fn main() {
    println("hello")
}
```

## `scripts/smoke.sh`

```bash
#!/usr/bin/env bash
set -euo pipefail

ALEF_BIN="${ALEF_BIN:-alef}"
"$ALEF_BIN" run main.alef
```

For server examples, the smoke script should:

1. bind a random localhost port
2. start `alef run main.alef`
3. call real HTTP endpoints
4. verify response bodies
5. call `/__shutdown`
6. exit non-zero on any mismatch
