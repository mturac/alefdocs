# Tutorial: Build an AI Workflow

This tutorial builds a support-ticket classifier with a deterministic AI
provider boundary.

## Classify Tickets

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
    if contains_any(text, ["timeout", "error", "500"]) {
        return "platform"
    }
    return "general"
}
```

## Add AI Summary

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

## Output JSON

```alef
fn main() {
    let ticket = {
        "id" => "TCK-1001",
        "title" => "Refund for duplicate invoice",
        "body" => "Customer was charged twice."
    }
    let queue = classify_ticket(ticket)
    println(json_encode({
        "id" => ticket["id"],
        "queue" => queue,
        "ai" => ai_summary(ticket, queue)
    }))
}
```
