# Results and Errors

Alef uses explicit values for operations that can fail.

```alef
fn divide(a: f64, b: f64) -> Result<f64, string> {
    if b == 0.0 {
        return Err("division by zero")
    }
    return Ok(a / b)
}
```

## `?`

The `?` operator unwraps `Ok(value)` and early-returns on `Err(error)`.

```alef
let x = divide(20.0, 4.0)?
let y = divide(x, 2.0)?
```

## HTTP Client Results

Native HTTP client calls return `Result<HttpResponse, string>`:

```alef
match std.http.get("https://example.com") {
    Ok(r) => println(r.body),
    Err(e) => println("request failed: {e}"),
}
```

This avoids silent network failures.
