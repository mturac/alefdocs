# What is Alef?

Alef is a programming language.

It includes:

- syntax
- modules
- types
- functions
- control flow
- errors as values
- a standard library
- a command-line tool
- a native runtime

Alef is AI-native because AI provider calls and agent-era protocols are part of
the standard library story. That does not make Alef an app framework. The
framework-like examples exist to prove that the language and runtime can build
real programs.

The default execution story is:

```bash
alef run main.alef
```

That command runs an Alef program on the native runtime. Public examples should
target this path unless they are specifically documenting the TypeScript
interpreter or Go codegen.

## Design Goals

Alef optimizes for language-level outcomes:

- readable syntax for scripts, services, and tools
- explicit `Result` and `Option` values for failure and absence
- useful data modeling with maps, structs, enums, and pattern matching
- a standard library that includes modern backend and AI surfaces
- a runtime that can execute real programs without a separate framework stack

## A Tiny Program

```alef
fn greet(name) {
    return "hello, {name}"
}

fn main() {
    println(greet("Alef"))
}
```

## A Tiny Backend Using The Language

```alef
import std.http { json_response }

fn with_state(response, state) {
    return { "response" => response, "state" => state }
}

fn health(request, state) {
    return with_state(json_response(json_encode({
        "ok" => true,
        "runtime" => "native"
    })), state)
}

fn app() {
    let app = std.http.with_state(std.http.app(), {})
    return std.http.route(app, "GET", "/health", health)
}

fn main() {
    std.http.listen_options("127.0.0.1:8090", app(), {
        "shutdown_path" => "/__shutdown"
    })
}
```

## What Alef Is Not

Alef is not a web framework. It can build web servers because the standard
library has HTTP primitives.

Alef is not an AI wrapper. It can call AI providers because the standard
library has AI provider primitives.

Alef is not just examples. TicketDesk and Agent Ticket Router are example
programs written in the language.

Alef is also not a promise that every mature Go, Rust, Python, or .NET library
already has an equivalent. The current strength is a compact, integrated
language and runtime path for useful programs.
