# Arrays and Maps

Arrays and maps are the everyday data structures for Alef backend code.

## Arrays

```alef
let statuses = ["triage", "progress", "review", "done"]
statuses.push("archived")
```

Iterate with `for`:

```alef
for status in statuses {
    println(status)
}
```

## Maps

Maps use `=>` for key/value pairs:

```alef
let ticket = {
    "id" => "TD-101",
    "title" => "Checkout timeout",
    "priority" => "P0"
}
```

Access with brackets:

```alef
println(ticket["title"])
```

## Nested Data

```alef
let state = {
    "selected" => "ops",
    "tickets" => [
        { "id" => "TD-101", "status" => "triage" }
    ]
}
```
