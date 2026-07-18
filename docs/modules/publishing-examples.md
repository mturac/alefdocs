# Publishing Example Repositories

Public Alef examples should feel complete when opened on GitHub.

Minimum files:

```text
README.md
LICENSE
AGENTS.md
alef.mod
main.alef
scripts/smoke.sh
```

## README Checklist

- what the example demonstrates
- how to run it with `ALEF_BIN`
- the main routes or commands
- the expected smoke command
- the Alef features shown

## Portability Rules

- no machine-local absolute paths
- no secrets
- no required live provider unless the repo is specifically about that provider
- no hidden setup step beyond `ALEF_BIN` or `alef` on `PATH`

## Good Example Bar

A good example mutates state or performs a real workflow. It should not be a
static mockup with a success message.
