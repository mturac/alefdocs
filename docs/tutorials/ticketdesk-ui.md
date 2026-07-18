# Tutorial: Build TicketDesk UI

TicketDesk is a real-life Alef example: a multi-workspace ticket and task
manager served by the native runtime.

It demonstrates:

- server-rendered UI
- multiple workspaces
- ticket columns
- assignment actions
- status movement
- activity feed
- JSON API verification

## Data Model

```alef
fn workspace_seed() {
    return [
        { "id" => "ops", "name" => "Ops Desk", "lead" => "Ada", "sla" => "4h" },
        { "id" => "product", "name" => "Product Bugs", "lead" => "Grace", "sla" => "1d" }
    ]
}

fn ticket_seed() {
    return [
        {
            "id" => "TD-101",
            "workspace" => "ops",
            "title" => "Checkout API timeout",
            "status" => "triage",
            "priority" => "P0",
            "assignee" => "ada"
        }
    ]
}
```

## Stateful UI Handler

```alef
import std.http { html }

fn with_state(response, state) {
    return { "response" => response, "state" => state }
}

fn page(request, state) {
    let body = "<!doctype html><html><body><h1>Alef TicketDesk</h1></body></html>"
    return with_state(html(body), state)
}
```

## Action Route

```alef
fn move_ticket(request, state) {
    let id = request["params"]["id"]
    let status = request["params"]["status"]
    let tickets = []

    for ticket in state["tickets"] {
        if ticket["id"] == id {
            tickets.push({
                "id" => ticket["id"],
                "workspace" => ticket["workspace"],
                "title" => ticket["title"],
                "status" => status,
                "priority" => ticket["priority"],
                "assignee" => ticket["assignee"]
            })
        } else {
            tickets.push(ticket)
        }
    }

    let next = {
        "workspaces" => state["workspaces"],
        "tickets" => tickets,
        "events" => state["events"],
        "selected" => state["selected"]
    }
    return with_state(html("<p>updated</p>"), next)
}
```

## Routes

```alef
fn app() {
    let app = std.http.with_state(std.http.app(), initial_state())
    let app = std.http.route(app, "GET", "/", page)
    let app = std.http.route(app, "GET", "/workspace/:id", workspace_page)
    let app = std.http.route(app, "GET", "/move/:id/:status", move_ticket)
    return std.http.route(app, "GET", "/api/tickets", tickets_json)
}
```

## Smoke Test Contract

A serious Alef UI example should prove:

- `GET /` returns real HTML
- a workspace switch updates the visible board
- move/assign routes mutate state
- `/api/tickets` exposes the changed state
- `/__shutdown` stops the server cleanly

That is why the public TicketDesk repo ships `scripts/smoke.sh`.
