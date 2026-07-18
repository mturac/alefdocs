# Release Notes

Documentation-facing release notes for public Alef users. Compiler and runtime
source stay private; this site is the public contract for learning and APIs.

## 2026-07-18 — AlefDocs + native maturity snapshot

### Public docs project

- Progress tracker: [Documentation Roadmap](docs-roadmap.md)

- Canonical public documentation is **AlefDocs**:
  [github.com/mturac/alefdocs](https://github.com/mturac/alefdocs)
- Live site: [mturac.github.io/alefdocs](https://mturac.github.io/alefdocs/)
- Full write-up: [What's New — July 2026](whats-new-2026-07.md)

### Runtime and stdlib (native `alef run`)

User-visible capability clusters closed and documented for the native path:

- **Crypto / random:** secure random, digests, HMAC-SHA256, AES, Ed25519, PBKDF2,
  Blake2, ECDSA, X.509-related helpers
- **Sync / concurrency:** atomics, mutex patterns, once, maps, pools, barriers,
  semaphores, `when_all` / `when_any`
- **Time / IO:** sleep, parse, mono clock, ticker; copy, read-all, limit, pipe,
  multi-writer, tee, seek
- **HTTP / encoding:** richer HTTP surfaces, cookie helpers, base64, gob/ASN.1
  related encoding work
- **Archive / embed:** zip/tar and embed-related helpers
- **AI agents:** chat, stream, tools, embeddings; jobs queue with retry and
  optional SQLite persistence hooks
- **Ops:** SSE, auth, metrics, circuit-breaker style advanced surfaces for
  native services

### Install

On macOS, after installing a release binary:

```bash
codesign --force -s - ./alef
alef --version
```

### Maturity note

Alef remains **AI-native and native-first**. It does not claim full Go or .NET
stdlib replacement. Prefer documented modules and tutorials over assuming
unlisted package parity.

---

## Native-first Docs

Public examples target:

```bash
alef run main.alef
```

## HTTP Client Result Behavior

Native HTTP client calls return `Result<HttpResponse, string>`:

```alef
match std.http.get("https://example.com") {
    Ok(r) => println(r.body),
    Err(e) => println("request failed: {e}"),
}
```

## Bytecode Strict Mode

Use strict bytecode checks when validating bytecode support:

```bash
alef --strict-bytecode run main.alef
```
