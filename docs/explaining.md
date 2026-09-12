# Explaining — Read-Only Code Understanding (`/explain-code`)

> Three lenses for understanding existing code. No code is modified.

## The Three Lenses (pick a/b/c, combinable)

| Lens | Skill | What It Produces | When to Pick |
|------|-------|------------------|--------------|
| (a) **Architecture** | `improve-codebase-architecture` (mattpocock, 915K) | HTML report + Mermaid — deep-module opportunities (Strong / Worth / Speculative), before/after diagrams, hot spots from `git log` | "Why is this codebase hard to change?" / pre-refactor triage |
| (b) **Schema** | `database-schema-designer` (softaworks) | ERD + table/relation spec + checklist | "How is the data modeled?" / pre-migration |
| (c) **Features** | `write-feature-docs` (warpdotdev) | Feature doc — purpose, entry points, files, user flow | "What does this feature do?" / onboarding |

## Flow

```
/explain-code
  → ask what to explain: (a) architecture, (b) schema, (c) features (or combo)
  → reconnaissance (read-only): git history, existing CONTEXT.md / ADRs, schema files
  → produce artifact:
      (a) → $TMPDIR/architecture-review-*.html (opened via xdg-open/open) — not in repo
      (b) → docs/schema.md (only if user asks to save) or inline ERD
      (c) → docs/features.md (only if user asks to save) or inline doc
  → if user wants to act on findings, suggest /spec
```

## Outputs

- **Temp (default for architecture):** `$TMPDIR/architecture-review-<timestamp>.html` — not committed.
- **Persisted (only on request):** `docs/explain/architecture-*.md`, `docs/explain/schema-*.md`, `docs/explain/features-*.md` or `docs/schema.md` / `docs/features.md` at repo root of the consumer project.

## Notes

- Exploring vs verifying: `with_server.py` and Mermaid generation are black-box tools — run `--help` first, don't read source until needed.
- All three lenses are **optional** — not part of the 6 CORE lifecycle commands.
