# Control Flow

## `if`

```alef
if priority == "P0" {
    return "incident-lead"
}
return "support"
```

Boolean operators:

```alef
if queue == "platform" and text.contains("timeout") {
    return "incident"
}
```

## `for`

```alef
for ticket in tickets {
    println(ticket["id"])
}
```

## `while`

```alef
let i = 0
while i < 10 {
    println(i)
    i = i + 1
}
```

## `match`

```alef
match result {
    Ok(value) => println(value),
    Err(error) => println("failed: {error}"),
}
```

## `stream` and `yield`

Alef supports streaming values lazily using `stream` and `yield`. A `stream` expression creates a lazy iterator that can be evaluated over time.

```alef
fn fibonacci(): stream {
    let a = 0;
    let b = 1;
    stream {
        yield a;
        let next = a + b;
        a = b;
        b = next;
    }
}
```

Use `for` to consume a stream:

```alef
for num in fibonacci() {
    if num > 100 {
        break;
    }
    println(num);
}
```
