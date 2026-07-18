# Syntax Reference

This page is a practical syntax reference for writing `.alef` programs. It is
public language documentation, not a description of the private compiler
implementation.

## File Shape

```alef
import std.http { json_response }

fn main() {
    println("hello")
}
```

Alef files usually contain imports, declarations, and statements inside
functions. The conventional program entrypoint is `main`.

## Comments

```alef
// A line comment explains the next statement.
println("ready")
```

## Primitive Values

```alef
let name = "Ada"
let count = 3
let ratio = 0.75
let active = true
let missing = none
```

## Strings

Strings use double quotes. Interpolation uses `{name}`.

```alef
let id = "TD-101"
println("ticket {id} loaded")
```

## Bindings

```alef
let name = "Ada"
name = "Grace"
```

Use reassignment for a real state transition. Use a new binding when the new
value has a distinct meaning.

## Function

```alef
fn add(a, b) {
    return a + b
}
```

## Typed Function

```alef
fn add(a: int, b: int) -> int {
    return a + b
}
```

## Decorator

Decorators attach supported metadata to the function that follows them.

```alef
@deprecated("use new_add instead")
fn old_add(a: int, b: int) -> int {
    return a + b
}

@inline
fn new_add(a: int, b: int) -> int {
    return a + b
}
```

Supported public decorators are `@test`, `@bench`, `@deprecated`, `@inline`,
and `@noinline`.

## Operators

```alef
let n = 1 + 2 * 3
let ok = n >= 3
let visible = ok and not hidden
let owner = plan == "enterprise" or priority == "P0"
```

Use `==` for equality. Use `and`, `or`, and `not` for boolean logic.

## Array

```alef
let xs = [1, 2, 3]
xs.push(4)
println(xs[0])
```

## Map

```alef
let ticket = {
    "id" => "TD-101",
    "status" => "triage"
}

println(ticket["status"])
```

## Struct

```alef
struct Ticket {
    id: string,
    title: string
}

let ticket = Ticket {
    id: "TD-101",
    title: "Checkout timeout"
}

println(ticket.title)
```

## Enum

```alef
enum Status {
    Triage,
    Progress,
    Done,
}

let status = Status.Triage
```

## If

```alef
if ok {
    return "yes"
}
return "no"
```

Use `else` when both branches produce useful work:

```alef
if priority == "P0" {
    println("page incident lead")
} else {
    println("queue normally")
}
```

## For

```alef
for item in items {
    println(item)
}
```

## While

```alef
while retries < 3 {
    retries = retries + 1
}
```

## Match

```alef
match value {
    Ok(v) => v,
    Err(e) => 0,
}
```

## Result

```alef
fn divide(a: f64, b: f64) -> Result<f64, string> {
    if b == 0.0 {
        return Err("division by zero")
    }
    return Ok(a / b)
}
```

## Option

```alef
fn find_owner(ticket) -> Option<string> {
    if ticket["owner"] == "" {
        return None
    }
    return Some(ticket["owner"])
}
```

## Import

```alef
import std.http { json_response }
```

## Complete Small Program

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
        "title" => "Checkout timeout",
        "plan" => "enterprise",
        "blocked" => true
    }

    let p = priority(ticket["plan"], ticket["blocked"])
    let id = ticket["id"]
    println("{id}: {p}")
}
```

## Advanced AI-Native

Alef is designed for AI workloads with DeepMind/JAX-inspired vectorization, differentiation, macros, and data streams.

```alef
// 1. Vectorization (vmap) and Differentiation (grad)
fn f(x) { x * 2.0 }
let vec_f = vmap(f)
let grad_f = grad(f)

// 2. Metaprogramming (macro)
macro html(content) {
    "<div class=\"ai-gen\">" + content + "</div>"
}
let ui = html!("Hello AI")

// 3. Async Streams (Generators)
fn stream_llm() {
    yield "Hello"
    yield "World"
}
for await chunk in stream_llm() {
    print(chunk)
}
```
