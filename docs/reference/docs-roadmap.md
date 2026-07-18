# Documentation Roadmap

This page is the **progress bar for public docs**. It says what learners can
already rely on, what is mid-flight, and what comes next — without treating
private compiler work as a completion metric.

Live site: [mturac.github.io/alefdocs](https://mturac.github.io/alefdocs/)  
Repo: [github.com/mturac/alefdocs](https://github.com/mturac/alefdocs)

**Updated:** 2026-07-18 (Phase 5 pages landed)

## How to read this

| Status | Meaning |
|--------|---------|
| **Done** | On the public site, linked from SUMMARY, usable today |
| **Now** | Current docs priority (next edits land here) |
| **Next** | Planned after Now; order may change |
| **Later** | Not scheduled; no false "coming soon" dates |

Private language/runtime source stays private. This roadmap is **docs-only**.

---

## Progress at a glance

```text
[███████████████░░░░░]  ~75% of public learning path

Done     Install · book · HTTP/AI/DB · crypto/sync/time/io/jobs refs · July 2026 notes
Now      Agent backend live polish · install binaries polish
Next     Cookbook expansion · language-spec gaps · searchable nav
Later    Full multi-language locales · generated API index · video track
```

| Phase | Theme | Status |
|-------|--------|--------|
| 0 | Public docs home (`alefdocs` + GitHub Pages) | **Done** |
| 1 | Zero-to-run path (install → first program → tour) | **Done** |
| 2 | Language book (syntax, data, errors, modules) | **Done** |
| 3 | Runtime + core stdlib (HTTP, JSON, DB, AI stub) | **Done** |
| 4 | July 2026 maturity snapshot (What's New, release notes) | **Done** |
| 5 | Stdlib depth (crypto, sync, time, io, jobs, cookies) | **Done** (expand in place) |
| 6 | Agent backend path (HTTP + AI + jobs + sessions) | **Now** |
| 7 | Cookbook & real-world recipes | **Next** |
| 8 | Spec completeness + navigability | **Next** |
| 9 | Packaging, multi-locale, generated API reference | **Later** |

---

## Phase 0 — Docs home · Done

- Separate public repo: `mturac/alefdocs` (not the private language tree)
- GitHub Pages: root of `main` → https://mturac.github.io/alefdocs/
- Branding: native-first, private source + public docs/binaries

## Phase 1 — Zero-to-run · Done

| Doc | Role |
|-----|------|
| Book 1–3 | Why Alef, install, first program |
| Quickstart / project structure | Fast path |
| FAQ / What is Alef | Orientation |

**Exit criteria met:** A new reader can install a binary, run `alef run main.alef`, and print output without a private checkout.

## Phase 2 — Language book · Done

| Doc | Role |
|-----|------|
| Book 4–8 | Values, control flow, collections, Result/Option, modules |
| Language tour + topic pages | Lookup |
| Autodiff / macros / composition | Advanced language notes |

**Exit criteria met:** Core syntax is teachable as a language, not only as samples.

## Phase 3 — Runtime and core stdlib · Done

| Doc | Role |
|-----|------|
| Book 9–13 | CLI, HTTP, DB/cache, AI, testing |
| Stdlib overview + HTTP/AI/DB refs | Module contract |
| Native API / TicketDesk / AI ticket router | Tutorials |

**Exit criteria met:** Learner can build a small HTTP service and call AI with `stub`.

## Phase 4 — July 2026 snapshot · Done

| Doc | Role |
|-----|------|
| [What's New — July 2026](whats-new-2026-07.md) | Capability summary |
| [Release notes](release-notes.md) | Chronological notes |
| Install: macOS `codesign` | Taskgated fix |

Honest maturity line (also on What's New): Alef is **AI-native + native-first**, not full Go/.NET stdlib parity.

## Phase 5 — Stdlib depth · Now → largely Done

Dedicated native-path reference pages:

1. [Crypto And Encoding](../stdlib/crypto-encoding.md) — **Done**
2. [Sync And Concurrent](../stdlib/sync-concurrent.md) — **Done**
3. [Time And IO](../stdlib/time-io.md) — **Done**
4. [Jobs](../stdlib/jobs.md) — **Done**
5. HTTP cookies / headers — in [HTTP reference](../stdlib/http-json.md) — **Done** (section)

**Exit:** Each cluster has a dedicated or clearly sectioned page with `alef run` examples.
Further depth (AES/Ed25519 recipes, full sync primitive catalog) can still expand in place.

## Phase 6 — Agent backend path · Now

| Work | Status |
|------|--------|
| [AI Agent Backend cookbook](../cookbook/ai-agent-backend.md) | E2E checklist **Done** |
| Multi-turn chat + stream notes | **Done** (stub-safe) |
| Sessions with `std.db` recipe | Sketch **Done** (wire to db-cache) |
| Jobs + dead-letter recipe | **Done** in cookbook + [Jobs](../stdlib/jobs.md) |

**Done when:** One end-to-end public recipe: chat API + history + stub AI + shutdown path, copy-pasteable from docs alone.

## Phase 7 — Cookbook expansion · Next

Planned recipes (not yet full pages):

1. Provider-gated live AI (keep stub default)
2. Rate limit / auth middleware sketches
3. SQLite migrations for sessions
4. Package/vendor sketch (`alef.mod`) for small libraries

## Phase 8 — Spec and navigation · Next

- Close gaps called out in language specification vs book
- Sidebar/nav parity: every SUMMARY entry has a `pages/*.html` twin
- On-site "Start here → What's new → Roadmap" footer on home

## Phase 9 — Later (no date)

- Generated API index from public binary surfaces
- TR/EN dual locale (only if content stays in sync)
- Optional video or short screencast index (external links only)

---

## What we will not track here

- Private LR-0 / inventory scaffold counts
- Closing "every Go package" as a docs success metric
- Undated "soon" claims without a phase row above

---

## Suggested reading order (stable)

1. [Install](../../book/02-installing-and-running.md)
2. [First program](../../book/03-your-first-program.md)
3. [Language tour](../language/tour.md)
4. [HTTP](../stdlib/http-json.md) → [AI](../stdlib/ai.md)
5. [What's New — July 2026](whats-new-2026-07.md)
6. **This roadmap** (you are here) for "what next"

---

## Change log (docs roadmap itself)

| Date | Note |
|------|------|
| 2026-07-18 | Initial roadmap; Phases 0–4 Done; 5–6 Now; 7–8 Next; 9 Later |
| 2026-07-18 | Phase 5 reference pages + agent-backend e2e cookbook expansion |
