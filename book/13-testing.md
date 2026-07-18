# 13. Testing Alef Programs

Alef supports tests and operational smoke scripts.

## Unit Tests

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

Public examples should include:

```bash
bash scripts/smoke.sh
```

A good smoke script exercises behavior. For a server program, it should:

1. start the server on localhost
2. request a real page or endpoint
3. trigger a state change
4. verify the state changed
5. call `/__shutdown`

That is how an example proves it is a program, not a screenshot.
