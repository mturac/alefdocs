# 6. Collections And Data Modeling

Programs need to hold more than one value. Alef gives beginners two simple
tools first:

- arrays for ordered lists
- maps for key/value data

When a shape deserves a name, use structs and enums.

## Arrays

An array stores values in order.

```alef
fn main() {
    let statuses = ["triage", "progress", "review", "done"]
    println(statuses[0])
}
```

Expected output:

```text
triage
```

Add an item with `push`:

```alef
fn main() {
    let statuses = ["triage", "progress"]
    statuses.push("done")

    for status in statuses {
        println(status)
    }
}
```

## Maps

A map stores values by key. This is useful for JSON-like data.

```alef
fn main() {
    let ticket = {
        "id" => "TD-101",
        "title" => "Checkout timeout",
        "priority" => "P0"
    }

    println(ticket["title"])
}
```

Expected output:

```text
Checkout timeout
```

Use maps when:

- data comes from JSON
- an example should be easy to inspect
- keys are dynamic

## Structs

Use a struct when a shape deserves a name.

```alef
struct Task {
    id: string,
    title: string,
    done: bool
}

fn main() {
    let task = Task {
        id: "task_1",
        title: "Write docs",
        done: false
    }

    println(task.title)
}
```

Structs make a program easier to read when the same shape appears many times.

## Enums

Use an enum when the valid cases are finite.

```alef
enum Status {
    Triage,
    Progress,
    Done,
}
```

Enums are useful for states because they prevent vague strings from spreading
through a program.

## Choosing The Right Shape

Use this rule of thumb:

- array: many values in order
- map: flexible key/value data
- struct: named fields with a stable shape
- enum: one value from a known set of cases

## Exercise

Create a map named `customer` with:

- `name`
- `plan`
- `blocked`

Write a function that returns `"review"` when the customer is blocked and
`"ok"` otherwise.
