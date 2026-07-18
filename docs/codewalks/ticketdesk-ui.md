# Codewalk: TicketDesk UI

TicketDesk is a multi-workspace ticket and task manager served by Alef native
HTTP.

## 1. State

The app starts with workspaces, members, tickets, events, and a selected
workspace.

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

## 2. UI Rendering

The UI is server-rendered HTML returned through `std.http.html`.

```alef
fn page(request, state) {
    return with_state(html(shell(state, state["selected"])), state)
}
```

## 3. Actions

Route params drive state changes:

```alef
let id = request["params"]["id"]
let status = request["params"]["status"]
```

## 4. Verification

The smoke script proves the workflow:

- open `/`
- switch workspace
- move a ticket
- assign a ticket
- verify `/api/tickets`
- shut down the server
