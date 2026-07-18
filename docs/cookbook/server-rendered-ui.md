# Cookbook: Server-rendered UI

Use `std.http.html` when an example needs a UI without a frontend build step.

```alef
import std.http { html }

fn with_state(response, state) {
    return { "response" => response, "state" => state }
}

fn home(request, state) {
    let body = "<!doctype html><html><body><h1>Hello</h1></body></html>"
    return with_state(html(body), state)
}
```

Wire it:

```alef
fn app() {
    let app = std.http.with_state(std.http.app(), {})
    return std.http.route(app, "GET", "/", home)
}
```

This pattern is ideal for public examples where the point is Alef's native
runtime, not a separate frontend toolchain.
