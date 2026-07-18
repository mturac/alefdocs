# Codewalk: Agent Ticket Router

The Agent Ticket Router is a small workflow for support triage.

## 1. Classify

```alef
fn classify_ticket(ticket) {
    let text = (ticket["title"] + " " + ticket["body"]).to_lower()
    if text.contains("refund") {
        return "billing"
    }
    return "general"
}
```

## 2. Prioritize

Enterprise and incident-like tickets become higher priority.

```alef
if ticket["plan"] == "enterprise" {
    return "p1"
}
```

## 3. AI Boundary

The example uses the deterministic stub provider:

```alef
let response = std.ai.response_with("stub", prompt)
```

## 4. JSON Contract

The program prints JSON so a smoke script can validate queue, priority, owner,
and provider.
