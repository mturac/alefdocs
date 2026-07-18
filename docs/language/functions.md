# Functions

Functions use `fn`.

```alef
fn add(a, b) {
    return a + b
}
```

## Typed Functions

```alef
fn format_ticket(id: string, title: string) -> string {
    return "{id}: {title}"
}
```

## Early Return

```alef
fn priority(plan, blocked) {
    if plan == "enterprise" and blocked {
        return "P0"
    }
    return "P2"
}
```

## Callback Functions

```alef
let upper = items.map(fn(item) {
    return item.to_upper()
})
```
