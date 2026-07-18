# Testing

Alef supports code-level tests and operational smoke tests.

## Alef Tests

```alef
@test
fn adds_numbers() {
    assert_eq(2 + 3, 5)
}
```

Run:

```bash
alef test .
```

## Smoke Tests

Public app examples should include `scripts/smoke.sh`.

For a server example, smoke tests should:

- start the server on localhost
- call real routes
- verify HTML or JSON
- mutate state
- verify the mutation through an API
- call `/__shutdown`

This is how the TicketDesk UI example proves it is not a static mockup.
