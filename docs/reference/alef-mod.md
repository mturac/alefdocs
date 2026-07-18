# alef.mod Reference

`alef.mod` names an Alef module.

```text
module ticketdesk

version 0.1.0
```

## `module`

The module name should be stable and portable.

```text
module agent-ticket-router
```

## `version`

Use semantic versioning for public examples and packages.

```text
version 0.1.0
```

## Public Repository Convention

Keep `alef.mod` simple. Do not encode local paths, credentials, or host-specific
configuration in the module file.
