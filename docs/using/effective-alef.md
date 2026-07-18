# Effective Alef

Effective Alef code is direct, smoke-testable, and honest about failure.

## Prefer Native-first Examples

Public examples should use:

```bash
alef run main.alef
```

Use interpreter or codegen paths only when that page is specifically about
those paths.

## Keep State Transitions Visible

Alef HTTP handlers return both the response and the next state:

```alef
return { "response" => response, "state" => next_state }
```

Use that shape to make workflow examples easy to test.

## Use `Result` For Failure

Network, provider, and database work can fail. Prefer values that show that:

```alef
match std.http.get("https://example.com") {
    Ok(r) => println(r.body),
    Err(e) => println("failed: {e}"),
}
```

## Make Examples Prove Behavior

Every public example should ship a smoke script. A good smoke script does not
only check that the program starts. It should exercise the workflow and verify
the result.

For UI examples:

- request the page
- trigger a state-changing action
- verify the UI or JSON state changed
- shut the server down cleanly

## Use Maps For Product Surfaces

Maps are convenient for JSON-heavy UI and API examples:

```alef
let ticket = { "id" => "TD-101", "status" => "triage" }
```

Use structs when the domain model needs a stable named shape.

## Keep Provider Calls Gated

Use `std.ai.response_with("stub", ...)` in docs and tests. Use live providers
only when credentials or local services are configured.
