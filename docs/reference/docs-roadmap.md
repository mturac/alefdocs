# Documentation Roadmap

Public docs are a **living product**. The install → book → core stdlib path is
shipped; everything after that is **actively expanding** — not a closed project
with a finish line.

This page is the progress tracker for [AlefDocs](https://mturac.github.io/alefdocs/).
Private language/runtime source stays private. Metrics here are **docs-only**.

Live: [mturac.github.io/alefdocs](https://mturac.github.io/alefdocs/) ·
Repo: [github.com/mturac/alefdocs](https://github.com/mturac/alefdocs)

**Updated:** 2026-07-18

## How to read this

| Status | Meaning |
|--------|---------|
| **Shipped** | On the public site today; keep polishing in place |
| **Building** | Active docs work right now |
| **Queued** | Next after Building; order can shift |
| **Horizon** | Direction of travel; no fake ship dates |

We will keep adding pages, recipes, and depth. A “Done” foundation does **not**
mean the docs stop growing.

---

## Two tracks

```text
FOUNDATION (shipped)          EXPANSION (ongoing → horizon)
[████████████] install, book,   [██░░░░░░░░░░░░░░░░░░░░] agent path,
               core stdlib,                   recipes, API index,
               July 2026 notes                locales, depth track…
```

| Track | What it means |
|-------|----------------|
| **Foundation** | A stranger can install, learn syntax, run HTTP + stub AI |
| **Expansion** | Deeper stdlib, production-shaped recipes, better nav, more surfaces |

Expansion is the long game. Expect this bar to move for a long time.

---

## At a glance

| # | Theme | Status |
|---|--------|--------|
| 0 | Public docs home (this site + GitHub Pages) | **Shipped** |
| 1 | Zero-to-run (install → first program) | **Shipped** |
| 2 | Language book (syntax through modules) | **Shipped** |
| 3 | Runtime + core stdlib (HTTP, JSON, DB, AI) | **Shipped** |
| 4 | July 2026 maturity snapshot | **Shipped** |
| 5 | Stdlib depth pages (crypto, sync, time, io, jobs) | **Shipped** · keep deepening |
| 6 | Agent backend path (chat + sessions + jobs) | **Building** |
| 7 | Cookbook: production-shaped recipes | **Building** / **Queued** |
| 8 | Spec gaps + navigation UX | **Queued** |
| 9 | Install & binary packaging polish | **Queued** |
| 10 | Generated API surface index | **Horizon** |
| 11 | Multi-locale (TR/EN) if we can keep them in sync | **Horizon** |
| 12 | Video / screencast index (external links) | **Horizon** |

---

## Foundation — shipped (keep polishing)

### Phase 0 — Docs home

- Separate public repo: `mturac/alefdocs`
- GitHub Pages from `main` → https://mturac.github.io/alefdocs/
- Native-first branding; private source + public docs/binaries

### Phase 1 — Zero-to-run

Book 1–3, quickstart, FAQ. Exit met: `alef run main.alef` without a private checkout.

### Phase 2 — Language book

Book 4–8, language tour, advanced notes. Exit met: core syntax teachable as a language.

### Phase 3 — Runtime and core stdlib

Book 9–13, HTTP/AI/DB refs, native API / TicketDesk tutorials. Exit met: small HTTP service + stub AI.

### Phase 4 — July 2026 snapshot

[What's New](whats-new-2026-07.md) · [Release notes](release-notes.md) · macOS `codesign` install note.

Honest line: **AI-native + native-first**, not full Go/.NET stdlib parity.

### Phase 5 — Stdlib depth (first pass shipped)

| Page | Status |
|------|--------|
| [Crypto And Encoding](../stdlib/crypto-encoding.md) | Shipped · more primitives later |
| [Sync And Concurrent](../stdlib/sync-concurrent.md) | Shipped · expand catalog |
| [Time And IO](../stdlib/time-io.md) | Shipped · more examples |
| [Jobs](../stdlib/jobs.md) | Shipped · persist/retry recipes |
| HTTP cookies/headers in [HTTP ref](../stdlib/http-json.md) | Shipped |

**Still to grow here:** AES/Ed25519 walkthroughs, full sync primitive catalog,
stream composition recipes, job dead-letter playbooks.

---

## Expansion — we are still building

### Phase 6 — Agent backend path · Building

Goal: one **copy-pasteable** public recipe — chat API + history + stub AI +
shutdown — from docs alone.

| Work | Status |
|------|--------|
| [AI Agent Backend cookbook](../cookbook/ai-agent-backend.md) | Skeleton + checklist shipped |
| Multi-turn chat (stub-safe) | Partial · deepen |
| Streaming chat notes | Partial · more examples |
| Sessions with `std.db` | Sketch · full runnable recipe next |
| Jobs + dead-letter in the same app | Partial · wire into one sample |

### Phase 7 — Cookbook expansion · Building / Queued

Recipes we intend to grow into full pages (not vapor — ordered by usefulness):

1. Provider-gated live AI (stub stays default for CI)
2. Rate limit + auth middleware sketches
3. SQLite migrations for chat sessions
4. `alef.mod` small-library / vendor sketch
5. Webhook + job retry patterns
6. Health, metrics, graceful shutdown checklist

### Phase 8 — Spec and navigation · Queued

- Close language-spec vs book gaps
- Every SUMMARY entry has a working `pages/*.html` twin
- Stronger “Start → Tour → Stdlib → Roadmap” path on the home page
- Searchable / filterable nav (when the site outgrows the sidebar)

### Phase 9 — Install and packaging polish · Queued

- Clearer binary install matrix (macOS arm64 / others as published)
- Version pinning and upgrade notes
- “Doctor / verify install” style page tied to public binaries

---

## Horizon — direction, not dates

| # | Direction |
|---|-----------|
| 10 | Generated API index from public binary surfaces |
| 11 | TR/EN dual locale **only if** content stays in sync |
| 12 | Optional video / screencast index (external links only) |
| + | More stdlib modules as they land on the public binary |
| + | More end-to-end apps (beyond TicketDesk / agent sketches) |

Horizon items get phase rows when work actually starts. No undated “soon”.

---

## What we will not track here

- Private compiler inventory / LR-0 style internal counts
- “Every Go package” as a docs success metric
- Fake completion percentages for the language itself

---

## Suggested reading order

1. [Install](../../book/02-installing-and-running.md)
2. [First program](../../book/03-your-first-program.md)
3. [Language tour](../language/tour.md)
4. [HTTP](../stdlib/http-json.md) → [AI](../stdlib/ai.md)
5. [What's New — July 2026](whats-new-2026-07.md)
6. **This roadmap** — what is shipping next on the public docs

---

## Change log

| Date | Note |
|------|------|
| 2026-07-18 | Initial roadmap |
| 2026-07-18 | Phase 5 stdlib pages + agent cookbook |
| 2026-07-18 | Reframe: foundation shipped, expansion ongoing (Building / Queued / Horizon) |
