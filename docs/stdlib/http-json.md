# HTTP and JSON

## Minimal Server

```alef
import std.http { json_response }

fn with_state(response, state) {
    return { "response" => response, "state" => state }
}

fn health(request, state) {
    return with_state(json_response(json_encode({ "ok" => true })), state)
}

fn app() {
    let app = std.http.with_state(std.http.app(), {})
    return std.http.route(app, "GET", "/health", health)
}

fn main() {
    std.http.listen_options("127.0.0.1:8090", app(), {
        "shutdown_path" => "/__shutdown"
    })
}
```

## App State And Middleware

Alef HTTP apps use state and middleware as the runtime composition boundary.
This is the Alef-style IoC surface: `main` wires the app, while `std.http`
calls your handlers and middleware for each request.

```alef
fn request_context(request, state) {
    let next_request = {
        "method" => request["method"],
        "path" => request["path"],
        "query" => request["query"],
        "headers" => request["headers"],
        "params" => request["params"],
        "body" => request["body"],
        "request_id" => "req-001"
    }
    return { "request" => next_request, "state" => state }
}

fn app_with_context(state) {
    let app = std.http.with_state(std.http.app(), state)
    return std.http.middleware(app, request_context)
}
```

Use this pattern for request IDs, auth guards, audit metadata, and other
cross-cutting HTTP behavior.

## Request Shape

Handlers receive a request map:

```alef
request["method"]
request["path"]
request["headers"]
request["query"]
request["params"]
request["body"]
```

## Responses

```alef
json_response(json_encode({ "ok" => true }))
problem_response(404, "not_found", "missing", "req-1")
html("<h1>Hello</h1>")
```

## Cookies

Helpers parse and format `Cookie` / `Set-Cookie` style header values:

```alef
// Parse an incoming Cookie header string into name/value pairs (map).
let cookies = std.http.parse_cookies(request["headers"]["cookie"])

// Format a cookie for Set-Cookie responses.
let header = std.http.format_cookie("session", "abc", {
    "path" => "/",
    "http_only" => true
})
```

Exact map keys may grow with releases; keep cookie values small and never store
secrets in client-readable cookies without encryption.

## Headers

```alef
let auth = std.http.get_header(request["headers"], "authorization")
```

## JSON

```alef
let body = json_encode({ "items" => [1, 2, 3] })
let value = json_decode(body)
println(value["items"][0])
```
