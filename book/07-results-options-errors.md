# 7. Results, Options, And Errors

Alef programs should make failure visible.

Instead of hiding failure in exceptions, Alef examples use values:

- `Ok(value)` for success
- `Err(error)` for failure
- `Some(value)` when a value exists
- `None` when it does not

## `Result`

Use `Result` when an operation can fail.

```alef
enum Result<T, E> {
    Ok(T),
    Err(E),
}

fn divide(a: f64, b: f64) -> Result<f64, string> {
    if b == 0.0 {
        return Err("division by zero")
    }
    return Ok(a / b)
}
```

Call it with `match`:

```alef
fn main() {
    match divide(10.0, 2.0) {
        Ok(v) => println("ok: {v}"),
        Err(e) => println("failed: {e}"),
    }
}
```

Expected output:

```text
ok: 5
```

## The `?` Operator

The `?` operator unwraps `Ok(value)` and returns early on `Err(error)`.

```alef
fn half_twice(n: f64) -> Result<f64, string> {
    let x = divide(n, 2.0)?
    let y = divide(x, 2.0)?
    return Ok(y)
}
```

Use `?` when the current function also returns a `Result`.

## `Option`

Use `Option` when a value might not exist.

```alef
enum Option<T> {
    Some(T),
    None,
}

fn owner(ticket) -> Option<string> {
    if ticket["owner"] == "" {
        return None
    }
    return Some(ticket["owner"])
}
```

Then match it:

```alef
match owner(ticket) {
    Some(name) => println(name),
    None => println("unassigned"),
}
```

## HTTP Failures

Native HTTP client calls return a `Result`.

```alef
match std.http.get("https://example.com") {
    Ok(r) => println(r.body),
    Err(e) => println("request failed: {e}"),
}
```

Network failure is not hidden. It is part of the program.

## Exercise

Write a function named `parse_priority` that returns:

- `Ok("P0")` when the input is `"urgent"`
- `Ok("P2")` when the input is `"normal"`
- `Err("unknown priority")` otherwise

Then call it with `match` and print either the parsed priority or the error.
