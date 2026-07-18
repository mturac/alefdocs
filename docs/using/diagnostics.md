# Diagnostics

Use the CLI before guessing.

## Health

```bash
alef health
```

Reports the runtime and high-level feature readiness.

## Doctor

```bash
alef doctor
```

Use this when a provider, runtime feature, or environment setup looks wrong.

## Smoke Scripts

For examples, prefer:

```bash
bash scripts/smoke.sh
```

A smoke script should print an exact success line, such as:

```text
ticketdesk ui smoke ok
```

If a check is optional because credentials are missing, print a clear skip
reason and exit successfully only when the provider is optional.
