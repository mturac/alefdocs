# 10. HTTP And JSON

HTTP and JSON are standard-library work in Alef.

## A Minimal Server

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

## Request Shape

Handlers receive a request map:

```alef
request["method"]
request["path"]
request["params"]
request["query"]
request["headers"]
request["body"]
```

## JSON

```alef
let body = json_encode({ "ok" => true })
let value = json_decode(body)
```

The same language features used for ordinary maps and arrays also describe
HTTP payloads.
