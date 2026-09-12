# Constraints — Quality Bar (`docs/CONSTRAINTS.md`)

> One written contract, enforced everywhere. Via `constraint-driven-development`.

## What It Is

A single file `docs/CONSTRAINTS.md` that every agent reads before changing code. Three tiers:

- **Floor** — things never allowed to weaken (no `@ts-ignore`/`eslint-disable` without record, no stubbed "Not implemented", no skipped tests, no checked-in secrets).
- **Enforced with numbers** — each dimension has a rule, a checker, and a timing:

| Dimension | Rule (default) | Checked by | Runs at |
|-----------|---------------|------------|---------|
| Types | 0 `tsc --noEmit` errors | `tsc` | every edit |
| Lint | 0 `eslint .` errors | `eslint` | every edit |
| Secrets | 0 findings | `gitleaks --redact` | every edit |
| Coverage | ≥80% of changed lines | `vitest --coverage` + `git diff` | per edit |
| Security code | 0 high severity | `semgrep` | per task + CI |
| Security deps | 0 high severity | `osv-scanner` / `npm audit` | CI |
| A11y | 0 critical | `axe` | per task |
| Perf | LCP ≤ 2500ms | `lighthouse` | per task |

- **Measured** — where the current bar sits ("Today" + direction).
- **Exceptions** — time-boxed waivers with owner + expiry (`W-42`, 2026-11-01). Expired exceptions fail the check.

## Lifecycle

```
/constraints  (once, or when the bar is undefined)
  → Detective pass: read package.json, configs, workflows
  → Interview: up to 4 questions, one per message ("Unknown" → default is applied)
  → Detect tools: tsc/eslint/gitleaks/semgrep/osv/axe/lighthouse
  → Install & wire:  check:fast (<5s) → check:task (<90s) → check:full (CI)
  → Write docs/CONSTRAINTS.md + patch AGENTS.md / CLAUDE.md + ratchets
  → Guard: git diff checks bar not lowered, flag new @ts-ignore, skipped tests
```

- **Ratcheting** — once a dimension hits 100%, it stays 100%. Use `/constraints check` or `/constraints ratchet`.
- **Enforcement** — every edit checks BUILD; every task checks VERIFY; PR/CI runs the full gate.

## File Location

Canonical: `docs/CONSTRAINTS.md` (legacy `CONSTRAINTS.md` at repo root is still read as fallback).
