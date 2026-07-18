# Language Tour

This tour shows Alef by building toward real backend code.

## Values

```alef
let service = "ticketdesk"
let retries = 3
let enabled = true
```

## Functions

```alef
fn label(id, title) {
    return "{id}: {title}"
}
```

## Collections

```alef
let ticket = {
    "id" => "TD-101",
    "title" => "Checkout timeout",
    "status" => "triage"
}

let tickets = [ticket]
```

## Loops

```alef
for ticket in tickets {
    println(ticket["id"])
}
```

## Branching

```alef
fn owner(priority) {
    if priority == "P0" {
        return "incident-lead"
    }
    return "support"
}
```

## Structs

```alef
struct Task {
    id: string,
    title: string,
    done: bool
}
```

## Results

```alef
fn divide(a: f64, b: f64) -> Result<f64, string> {
    if b == 0.0 {
        return Err("division by zero")
    }
    return Ok(a / b)
}
```

## Native HTTP

```alef
import std.http { json_response }

fn with_state(response, state) {
    return { "response" => response, "state" => state }
}

fn health(request, state) {
    return with_state(json_response(json_encode({ "ok" => true })), state)
}
```

Alef handlers return a response and the next state. This makes stateful smoke
tests straightforward.
