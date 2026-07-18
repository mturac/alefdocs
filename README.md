# AlefDocs

Public documentation site for **AlefLang** — separate from the private language/runtime repository (`mturac/aleflang`).

- Site: https://mturac.github.io/alefdocs/
- Source of truth for learners: this repo only (no private checkout required)

## Local preview

```bash
# any static server from repo root
python3 -m http.server 8765
# open http://127.0.0.1:8765/
```

## Deploy

GitHub Pages serves the repo root (`main` branch). Push to `main` updates the site.

## Relationship

| Repo | Role |
|------|------|
| `mturac/aleflang` | Language + native runtime (private) |
| `mturac/alefdocs` | Public docs / GitHub Pages (this project) |
| `mturac/aleflang-docs` | Earlier docs mirror (superseded by alefdocs) |
