# Variables and Values

Alef uses `let` for local bindings.

```alef
let name = "Ada"
let count = 3
let ready = true
```

Bindings can be reassigned in workflow code:

```alef
let status = "triage"
status = "progress"
```

## Common Value Kinds

```alef
let title = "Checkout timeout"
let retries = 3
let ratio = 0.75
let active = true
let missing = null
```

## Interpolation

```alef
let id = "TD-101"
println("ticket {id} opened")
```
