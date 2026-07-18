# Developing Modules

An Alef module starts with `alef.mod`.

```text
module ticketdesk

version 0.1.0
```

Recommended repository shape:

```text
ticketdesk/
├── alef.mod
├── main.alef
├── README.md
└── scripts/
    └── smoke.sh
```

## Naming

Use lowercase, hyphenated names for public example repositories:

```text
alef-ticketdesk-ui
alef-agent-ticket-router
```

## Smoke Test

Every module intended for public use should include:

```bash
bash scripts/smoke.sh
```

The smoke script is the trust boundary. It proves the README is not just prose.
