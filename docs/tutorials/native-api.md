# Tutorial: Build a Native API

This tutorial builds a small JSON API.

## 1. Create State

```alef
fn initial_state() {
    return {
        "accounts" => [
            { "id" => "acct_ada", "name" => "Ada AI Studio" }
        ]
    }
}
```

## 2. Create A Handler

```alef
import std.http { json_response }

fn with_state(response, state) {
    return { "response" => response, "state" => state }
}

fn list_accounts(request, state) {
    return with_state(json_response(json_encode({
        "data" => state["accounts"]
    })), state)
}
```

## 3. Wire Routes

```alef
fn app() {
    let app = std.http.with_state(std.http.app(), initial_state())
    return std.http.route(app, "GET", "/api/accounts", list_accounts)
}
```

## 4. Listen

```alef
fn main() {
    std.http.listen_options("127.0.0.1:8090", app(), {
        "shutdown_path" => "/__shutdown"
    })
}
```

Run:

```bash
alef run main.alef
```
