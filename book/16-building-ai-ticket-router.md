# 16. Building An AI Ticket Router

This chapter walks through a small AI-assisted program.

## Classification

```alef
fn contains_any(text, words) {
    for word in words {
        if text.contains(word) {
            return true
        }
    }
    return false
}

fn classify_ticket(ticket) {
    let text = (ticket["title"] + " " + ticket["body"]).to_lower()
    if contains_any(text, ["invoice", "payment", "refund"]) {
        return "billing"
    }
    if contains_any(text, ["login", "password", "2fa"]) {
        return "identity"
    }
    return "general"
}
```

## AI Boundary

```alef
fn ai_summary(ticket, queue) {
    let prompt = "Summarize ticket " + ticket["id"] + " for " + queue
    let response = std.ai.response_with("stub", prompt)
    return {
        "provider" => response.provider,
        "model" => response.model,
        "finish_reason" => response.finish_reason,
        "text_len" => len(response.text)
    }
}
```

## JSON Output

```alef
println(json_encode({
    "id" => ticket["id"],
    "queue" => queue,
    "ai" => ai_summary(ticket, queue)
}))
```

The `stub` provider keeps the example deterministic. The program can later be
configured for live providers without rewriting the language-level workflow.
