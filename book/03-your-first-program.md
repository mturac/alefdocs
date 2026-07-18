# 3. Your First Alef Program

In this chapter, you will build a tiny ticket priority program. It is small
enough to understand, but it uses the pieces you need in real Alef code:
values, functions, maps, `if`, and output.

## Step 1: Print Text

Create `main.alef`:

```alef
fn main() {
    println("TicketDesk")
}
```

Run it:

```bash
alef run main.alef
```

Expected output:

```text
TicketDesk
```

## Step 2: Store A Value

Change the file:

```alef
fn main() {
    let title = "Checkout timeout"
    println(title)
}
```

`let` creates a local value. `title` is the name. `"Checkout timeout"` is a
string.

Expected output:

```text
Checkout timeout
```

## Step 3: Use A Function

Functions make behavior reusable.

```alef
fn label(id, title) {
    return "{id}: {title}"
}

fn main() {
    println(label("TD-101", "Checkout timeout"))
}
```

Expected output:

```text
TD-101: Checkout timeout
```

## Step 4: Make A Decision

Use `if` when a program needs to choose.

```alef
fn priority(plan, blocked) {
    if plan == "enterprise" and blocked {
        return "P0"
    }
    return "P2"
}

fn main() {
    println(priority("enterprise", true))
}
```

Expected output:

```text
P0
```

## Step 5: Put Data In A Map

Maps are good for JSON-like data.

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

Expected output:

```text
TD-101: P0
```

You now know enough to read the next chapters:

- `fn` declares a function.
- `let` binds a value.
- strings use double quotes.
- maps use `"key" => value`.
- map reads use `ticket["id"]`.
- `if` branches on a condition.
- `and` combines boolean conditions.
- `return` exits a function with a value.
