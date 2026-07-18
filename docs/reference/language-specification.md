# Alef Language Specification

This is the public specification for Alef source programs. It describes the
language contract a user can rely on when writing `.alef` files. It is not a
description of the private compiler or native runtime implementation.

The specification is intentionally stricter than the tutorial pages. Tutorials
teach the path. This document defines the surface.

## Source Files

Alef source files use the `.alef` extension.

A source file contains zero or more imports and declarations. Executable
programs normally define `main`.

```alef
import std.http { json_response }

fn main() {
    println("hello")
}
```

## Notation

Examples in this document use ordinary Alef source. Grammar fragments are
written informally until the language grammar is published as a machine-readable
artifact.

Names in `code` are literal tokens or language constructs.

## Lexical Elements

Alef programs are written as Unicode text.

Whitespace separates tokens and is otherwise insignificant outside strings.
Newlines are accepted between statements and declarations. Semicolons are not
required in the beginner-facing style used by this book.

### Comments

Line comments begin with `//` and continue to the end of the line.

```alef
// This is a comment.
println("ready")
```

### Identifiers

Identifiers name values, functions, parameters, struct fields, enum variants,
and imported bindings.

```alef
let ticket_id = "TD-101"
fn priority(plan, blocked) { ... }
```

Public examples should prefer readable names over abbreviations.

### Keywords

The core keywords used in this book are:

```text
fn let return if else for in while match struct enum import true false none
and or not
```

Standard-library names such as `std.http` are not keywords.

### Literals

Alef supports:

- string literals: `"hello"`
- integer literals: `42`
- floating-point literals: `3.14`
- booleans: `true`, `false`
- none/null-like value: `none`
- arrays: `[1, 2, 3]`
- maps: `{ "id" => "TD-101" }`

## Strings

Strings use double quotes.

```alef
let name = "Ada"
```

String interpolation inserts values with braces.

```alef
println("hello, {name}")
```

For complex expressions, bind a value first and interpolate the name.

```alef
let id = ticket["id"]
println("{id}: ready")
```

## Declarations

### Function Declarations

Functions are declared with `fn`.

```alef
fn add(a, b) {
    return a + b
}
```

Typed signatures may be used when the program benefits from explicit contracts.

```alef
fn label(id: string, title: string) -> string {
    return "{id}: {title}"
}
```

The conventional executable entrypoint is:

```alef
fn main() {
    println("hello")
}
```

### Decorator Declarations

Decorators attach supported metadata to the following function declaration.

```alef
@deprecated("use new_priority instead")
fn old_priority(plan, blocked) {
    if plan == "enterprise" and blocked {
        return "P0"
    }
    return "P2"
}
```

Documented decorators are:

- `@test`
- `@bench`
- `@deprecated`
- `@inline`
- `@noinline`

Decorators are declaration metadata. Alef does not specify arbitrary aspect
weaving or hidden function-body rewriting as part of the public contract.

### Struct Declarations

A struct declares a named record shape.

```alef
struct Ticket {
    id: string,
    title: string,
    blocked: bool
}
```

Construct a struct with named fields.

```alef
let ticket = Ticket {
    id: "TD-101",
    title: "Checkout timeout",
    blocked: true
}
```

Read a field with dot access.

```alef
println(ticket.title)
```

### Enum Declarations

An enum declares a finite set of cases.

```alef
enum Status {
    Triage,
    Progress,
    Done,
}
```

Enum variants may carry values.

```alef
enum Shape {
    Circle(f64),
    Rect(f64, f64),
    Point,
}
```

## Statements

### Let Statements

`let` binds a local value.

```alef
let status = "triage"
```

Bindings may be reassigned when a program is modeling a state transition.

```alef
status = "progress"
```

### Return Statements

`return` exits the current function.

```alef
fn owner(priority) {
    if priority == "P0" {
        return "incident-lead"
    }
    return "support"
}
```

### If Statements

`if` selects a branch based on a boolean condition.

```alef
if blocked {
    return "P0"
}
return "P2"
```

`else` may be used when both branches are useful.

```alef
if blocked {
    println("needs attention")
} else {
    println("moving")
}
```

### For Statements

`for` iterates over iterable values such as arrays.

```alef
for ticket in tickets {
    println(ticket["id"])
}
```

### While Statements

`while` repeats while its condition is true.

```alef
while retries < 3 {
    retries = retries + 1
}
```

### Match Statements

`match` selects a branch by value shape.

```alef
match result {
    Ok(value) => println(value),
    Err(error) => println("failed: {error}"),
}
```

`match` is the preferred way to handle `Result`, `Option`, and enums in public
examples.

## Expressions

Expressions produce values.

### Calls

```alef
println("hello")
priority("enterprise", true)
```

### Operators

Arithmetic:

```alef
let total = subtotal + tax
let next = count + 1
```

Comparison:

```alef
let ok = priority == "P0"
let retry = attempts < 3
```

Boolean logic:

```alef
let urgent = blocked and plan == "enterprise"
let visible = not hidden
```

Boolean operators use words: `and`, `or`, and `not`.

### Arrays

```alef
let statuses = ["triage", "progress", "done"]
println(statuses[0])
```

Arrays preserve order and can be traversed with `for`.

### Maps

Maps use `=>` for key/value pairs.

```alef
let ticket = {
    "id" => "TD-101",
    "blocked" => true
}
```

Map values are read with bracket access.

```alef
println(ticket["id"])
```

Maps are the natural shape for JSON-like data and beginner examples.

## Types

The public type names used in this book include:

```text
string int f64 bool
```

Collection and algebraic shapes include:

```text
[T]
Result<T, E>
Option<T>
```

Struct and enum declarations introduce named types.

## Result

`Result<T, E>` represents success or failure.

```alef
enum Result<T, E> {
    Ok(T),
    Err(E),
}
```

Use `Result` when an operation can fail.

```alef
fn divide(a: f64, b: f64) -> Result<f64, string> {
    if b == 0.0 {
        return Err("division by zero")
    }
    return Ok(a / b)
}
```

The `?` operator unwraps `Ok(value)` and returns early on `Err(error)`.

```alef
fn half_twice(n: f64) -> Result<f64, string> {
    let x = divide(n, 2.0)?
    let y = divide(x, 2.0)?
    return Ok(y)
}
```

## Option

`Option<T>` represents a value that may be present or absent.

```alef
enum Option<T> {
    Some(T),
    None,
}
```

Use `Option` when missing data is expected.

## Imports And Modules

Imports bring names into scope.

```alef
import std.http { json_response }
```

Standard-library modules are part of the public language surface. The private
compiler and runtime source are not required to use them.

## Composition And Inversion Of Control

Alef programs can use inversion of control through runtime boundaries such as
the HTTP app, route handlers, middleware, state, tests, and benchmark runners.

The public language contract favors explicit composition over hidden
auto-wiring:

```alef
fn make_service(clock) {
    return { "clock" => clock }
}

fn main() {
    let service = make_service("2026-06-28T10:00:00Z")
    println(service["clock"])
}
```

There is no documented built-in dependency injection container. Pass
dependencies through parameters, app state, and small composition functions.

## Program Execution

Run a file with:

```bash
alef run main.alef
```

The shorter form also runs a file:

```bash
alef main.alef
```

This documentation prefers the explicit `run` form.

## Complete Example

```alef
fn priority(plan, blocked) {
    if plan == "enterprise" and blocked {
        return "P0"
    }
    return "P2"
}

fn main() {
    let ticket = {
        "id" => "TD-101",
        "plan" => "enterprise",
        "blocked" => true
    }

    let p = priority(ticket["plan"], ticket["blocked"])
    let id = ticket["id"]
    println("{id}: {p}")
}
```

Expected output:

```text
TD-101: P0
```

## Stability

This specification defines the documented public contract for the current
release candidate. If implementation behavior differs from this page, treat
the mismatch as a documentation or runtime bug to be fixed.
