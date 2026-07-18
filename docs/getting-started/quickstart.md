# Quickstart

This quickstart is the shortest path from no Alef knowledge to a running
program.

## 1. Create A Folder

```bash
mkdir alef-learning
cd alef-learning
```

## 2. Create `main.alef`

```alef
fn main() {
    let name = "Alef"
    println("Hello, {name}")
}
```

## 3. Run It

```bash
alef run main.alef
```

Expected output:

```text
Hello, Alef
```

## 4. Add A Function

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

## 5. Add Data

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

## What You Just Learned

- `fn main()` is where the program starts.
- `let` creates a value.
- strings use double quotes.
- `{name}` inserts a value into a string.
- maps use `"key" => value`.
- `ticket["id"]` reads from a map.
- `if` chooses between paths.
- `and` combines boolean checks.
- `return` sends a value back from a function.

Next, read the [Language Tour](../language/tour.md), then the book chapters on
syntax, control flow, collections, and errors.
