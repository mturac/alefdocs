# 15. Building TicketDesk UI

TicketDesk is a complete example program. It is a multi-workspace ticket and
task manager served by Alef native HTTP.

It exists to demonstrate the language in a real program:

- maps and arrays for state
- functions for rendering
- route params for actions
- state transitions
- JSON APIs
- a smoke script that verifies behavior

## State

```alef
fn initial_state() {
    return {
        "workspaces" => workspace_seed(),
        "members" => member_seed(),
        "tickets" => ticket_seed(),
        "events" => ["TD-101 opened by support intake"],
        "selected" => "ops"
    }
}
```

## UI Handler

```alef
import std.http { html }

fn page(request, state) {
    return with_state(html(shell(state, state["selected"])), state)
}
```

## Action Route

```alef
fn move_ticket(request, state) {
    let id = request["params"]["id"]
    let status = request["params"]["status"]
    // build next state
}
```

## Why This Example Matters

The example is not here because Alef is a ticketing framework. It is here
because a language should be able to express a non-trivial program clearly.
