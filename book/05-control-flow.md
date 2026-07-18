# 5. Control Flow

Control flow is how a program decides what happens next.

Alef has four beginner-level control-flow tools:

- `if` for decisions
- `for` for walking through a collection
- `while` for repeating until a condition changes
- `match` for choosing by value shape

## `if`

Use `if` when there are two or more possible paths.

```alef
fn owner(priority) {
    if priority == "P0" {
        return "incident-lead"
    }
    return "support"
}

fn main() {
    println(owner("P0"))
}
```

Expected output:

```text
incident-lead
```

Boolean operators use words:

```alef
fn route(queue, text) {
    if queue == "platform" and text.contains("timeout") {
        return "incident"
    }
    return "normal"
}
```

Read that condition as ordinary language:

```text
if queue is platform and text contains timeout
```

## `if` With `else`

Use `else` when both branches do real work.

```alef
fn message(blocked) {
    if blocked {
        return "needs attention"
    } else {
        return "moving"
    }
}
```

If the first branch returns, you can often skip `else` and keep the code flat.

## `for`

Use `for` to walk through arrays.

```alef
fn main() {
    let tickets = ["TD-101", "TD-102", "TD-103"]

    for ticket in tickets {
        println(ticket)
    }
}
```

Expected output:

```text
TD-101
TD-102
TD-103
```

Inside the loop, `ticket` is the current item.

## `while`

Use `while` when you need to repeat until a condition becomes false.

```alef
fn main() {
    let retries = 0

    while retries < 3 {
        println("try {retries}")
        retries = retries + 1
    }
}
```

`while` loops must change something inside the loop. Otherwise they can run
forever.

## `match`

Use `match` when the shape of a value matters.

```alef
match result {
    Ok(value) => println(value),
    Err(error) => println("failed: {error}"),
}
```

`match` is most useful with:

- `Result`
- `Option`
- enums

## Exercise

Write a function named `sla`:

- return `"1 hour"` for `P0`
- return `"4 hours"` for `P1`
- return `"next day"` for anything else

Then call it from `main`.
