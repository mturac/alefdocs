# 1. Learning Alef From Zero

This chapter is for the reader who opens the docs and asks: "What do I do
first?"

Alef is a programming language. That means you write source files, run them
with a command, and build programs out of values, functions, control flow,
data, and modules.

An Alef file usually looks like this:

```alef
fn main() {
    println("hello, Alef")
}
```

Save it as `main.alef`, then run:

```bash
alef run main.alef
```

Expected output:

```text
hello, Alef
```

That is the basic loop:

1. Edit a `.alef` file.
2. Run it.
3. Read the output or error.
4. Change the program.

## What A Program Is

A program is a set of instructions for the runtime. In Alef, the runtime starts
with `main`.

```alef
fn main() {
    let name = "Ada"
    println("hello, {name}")
}
```

Line by line:

- `fn main()` declares a function named `main`.
- `{ ... }` marks the body of the function.
- `let name = "Ada"` creates a local value.
- `println(...)` writes text to the terminal.
- `{name}` inside the string inserts the value of `name`.

## The Four Things To Learn First

Every beginner should learn these before standard-library details:

1. Values: strings, numbers, booleans, arrays, maps.
2. Functions: named blocks of reusable behavior.
3. Control flow: `if`, `for`, `while`, and `match`.
4. Data modeling: maps for flexible data, structs/enums for named shapes.

This book teaches those in that order.

## Alef Is Not The Source Repository

The public Alef experience is:

- the `alef` command
- `.alef` source files
- this language book
- public examples and release binaries

The compiler and native runtime implementation can remain private. A user does
not need to read the private source tree to learn or run Alef programs.

## What Makes Alef Different

Alef tries to make modern backend work feel like ordinary language work:

- JSON should not require a project ceremony.
- HTTP should feel like a standard-library feature.
- failures should be explicit with `Result`.
- AI provider calls should be documented as a standard-library surface, not as
  a separate app template.

That comes later. First, write and run small programs.
