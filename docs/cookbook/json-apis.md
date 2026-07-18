# Cookbook: JSON APIs

```alef
import std.http { json_response, problem_response }

fn with_state(response, state) {
    return { "response" => response, "state" => state }
}

fn list_tickets(request, state) {
    return with_state(json_response(json_encode({
        "data" => state["tickets"],
        "count" => len(state["tickets"])
    })), state)
}

fn get_ticket(request, state) {
    let id = request["params"]["id"]
    for ticket in state["tickets"] {
        if ticket["id"] == id {
            return with_state(json_response(json_encode({ "data" => ticket })), state)
        }
    }
    return with_state(problem_response(404, "not_found", "ticket not found", "req-1"), state)
}
```

Prefer JSON APIs that are verified by smoke tests.
