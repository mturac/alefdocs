# Strings

Strings use double quotes.

```alef
let name = "Alef"
```

## Interpolation

```alef
let service = "TicketDesk"
println("{service} is live")
```

## Useful Methods

```alef
let text = "API timeout".to_lower()
let urgent = text.contains("timeout")
let words = "triage,progress,done".split(",")
let clean = "  padded  ".trim()
```

Use string helpers for routing and classification workflows before reaching for
heavier parsing.
