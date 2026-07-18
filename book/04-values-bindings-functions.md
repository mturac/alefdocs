# 4. Syntax Fundamentals

This chapter teaches the core syntax you need before reading the standard
library or the larger examples.

Alef programs are plain text files ending in `.alef`. A program is made of
imports, declarations, and statements. The usual entrypoint is `main`.

```alef
fn main() {
    println("hello")
}
```

Blocks use braces. Statements are newline-oriented, so simple examples do not
need semicolons.

## Comments

Use `//` for a line comment.

```alef
// This runs when the program starts.
fn main() {
    println("ready")
}
```

## Values

Alef has strings, integers, floats, booleans, arrays, maps, structs, enums,
`Result`, and `Option`.

```alef
let name = "Ada"
let count = 3
let ratio = 0.75
let ready = true
```

Strings support interpolation with `{name}`:

```alef
let id = "TD-101"
println("ticket {id} loaded")
```

## Bindings

Use `let` for local bindings.

Bindings can be reassigned when a program needs to move state forward:

```alef
let status = "triage"
status = "progress"
```

Prefer reassignment when the program is modeling an actual state transition.
Prefer new names when each value has a distinct meaning.

## Functions

```alef
fn add(a, b) {
    return a + b
}
```

Typed signatures are available when they clarify the program:

```alef
fn label(id: string, title: string) -> string {
    return "{id}: {title}"
}
```

Functions are called with parentheses:

```alef
let text = label("TD-101", "Checkout timeout")
println(text)
```

## Early Returns

```alef
fn priority(plan, blocked) {
    if plan == "enterprise" and blocked {
        return "P0"
    }
    return "P2"
}
```

## Operators

Alef supports common arithmetic, comparison, and boolean operators:

```alef
let total = subtotal + tax
let retry = attempts < 3
let urgent = priority == "P0" or customer == "enterprise"
let ready = not blocked and assigned
```

Use `==` for equality. Use `and`, `or`, and `not` for boolean logic.

## Imports

Imports bring standard-library names into scope:

```alef
import std.http { json_response }

fn health(request, state) {
    return json_response("{\"ok\":true}")
}
```

The standard library is documented as part of the public language surface. The
private compiler and runtime source are not needed to use these imports.
