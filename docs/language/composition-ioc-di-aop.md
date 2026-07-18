# Composition, IoC, DI, And AOP

Alef supports the useful parts of inversion of control without hiding the
program behind a large framework.

The Alef style is:

- build dependencies in one visible place
- pass dependencies explicitly
- keep request state in `std.http.with_state`
- use middleware for request-wide behavior
- use decorators for supported declaration metadata

Alef does not currently document a Spring-style dependency injection container,
automatic class scanning, or a full aspect weaver. The point is to keep services
small enough that the composition remains readable.

## Alef-Style IoC

Inversion of control means your program describes handlers and boundaries, then
the runtime calls those handlers at the right time.

For HTTP programs, the app owns routes and middleware. The runtime owns the
request loop.

```alef
fn with_state(response, state) {
    return { "response" => response, "state" => state }
}

fn health(request, state) {
    return with_state(std.http.json_response(json_encode({
        "ok" => true
    })), state)
}

fn build_app(deps) {
    let app = std.http.with_state(std.http.app(), deps)
    return std.http.route(app, "GET", "/health", health)
}

fn main() {
    let deps = { "service" => "ticketdesk" }
    std.http.listen_options("127.0.0.1:8090", build_app(deps), {
        "shutdown_path" => "/__shutdown"
    })
}
```

The inversion is real: `main` wires the app, but `std.http` calls `health`.
The dependency graph is still visible in source.

## Dependency Injection

Prefer explicit dependency injection through parameters and state maps.

```alef
fn make_ticket_service(clock, id_prefix) {
    return {
        "clock" => clock,
        "id_prefix" => id_prefix
    }
}

fn create_ticket(service, title) {
    let prefix = service["id_prefix"]
    let clock = service["clock"]
    return {
        "id" => "{prefix}-101",
        "title" => title,
        "created_at" => clock
    }
}

fn main() {
    let service = make_ticket_service("2026-06-28T10:00:00Z", "TD")
    let ticket = create_ticket(service, "Checkout timeout")
    println(ticket["id"])
}
```

Run it:

```bash
alef run main.alef
```

Expected output:

```text
TD-101
```

This gives you testable code without hidden global state. In tests or smoke
programs, pass a deterministic clock, a fake provider, or an in-memory store.

## Middleware As Cross-Cutting Behavior

Middleware is the Alef-native place for request-wide behavior such as
authentication, request context, audit metadata, or rate limits.

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

fn build_app(state) {
    let app = std.http.with_state(std.http.app(), state)
    let app = std.http.middleware(app, request_context)
    return app
}
```

That is the Alef answer to most AOP use cases: put the cross-cutting behavior at
the boundary where it is observable and testable.

## Decorators

Alef has declaration decorators for supported function metadata and runners.

```alef
@deprecated("use new_priority instead")
fn old_priority(plan, blocked) {
    if plan == "enterprise" and blocked {
        return "P0"
    }
    return "P2"
}

@inline
fn add(a: int, b: int) -> int {
    return a + b
}

fn main() {
    println(old_priority("enterprise", true))
    println(add(1, 2))
}
```

Documented decorators are:

- `@test` for test discovery
- `@bench` for benchmark discovery
- `@deprecated` for deprecation metadata
- `@inline` and `@noinline` for optimization hints

Decorators are not a license to hide business logic. Use them for metadata and
runner integration; use middleware and explicit functions for behavior.

## Practical Rule

If you are deciding between a container and plain Alef composition, start with
plain Alef composition:

1. `main` builds dependencies.
2. `build_app` wires runtime boundaries.
3. handlers accept `request` and `state`.
4. middleware handles cross-cutting request behavior.
5. tests replace dependencies by passing different values.

That gives Alef an IoC story without making the language feel like a framework
you have to fight.
