# 8. Modules And Project Structure

An Alef project starts with a small shape:

```text
my-alef-program/
├── alef.mod
├── main.alef
├── README.md
└── scripts/
    └── smoke.sh
```

## `alef.mod`

```text
module my-alef-program

version 0.1.0
```

## Imports

Import names from a module:

```alef
import std.http { html, json_response }
```

Or use qualified names:

```alef
std.http.listen_options(address, app(), options)
```

## Public Example Rule

If a repo is meant to teach Alef, it should include a smoke script. The script
is proof that the README is true.
