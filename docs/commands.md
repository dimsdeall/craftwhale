# Commands — 6 CORE + 2 OPTIONAL

> `commands/*.toml` — slash commands registered via `npx skills add` (agenticskills.io format).

## Overview

| # | Command | Layer | Purpose |
|---|---------|-------|---------|
| 0 | `/constraints` | **OPTIONAL** — setup | Define & enforce quality bar → `docs/CONSTRAINTS.md` |
| 1 | `/spec` | CORE | Idea + PRD (WHAT & WHY) → `docs/specs/active/<id>/prd.md` |
| 2 | `/plan` | CORE | Impl plan (HOW) + ordered tasks (ORDER) |
| 3 | `/build` | CORE | Incremental code, TDD, 1 commit per task |
| 4 | `/verify` | CORE | Prove it works (tests, debug, security, perf) |
| 5 | `/review` | CORE | Persona-based review + ADR |
| 6 | `/ship` | CORE | Orchestrated release + archive |
| 7 | `/explain-code` | **OPTIONAL** — read-only | Explain architecture / schema / features |

## CORE — per-feature lifecycle

### `/spec` — SPEC → `prd.md`

- **Flow:** `brainstorming` hard-gate (Spike/Bounded/Architectural, one question at a time, diverge→converge, 95% confidence) → `idea-refine` → `interview-me` → present concept → approval → write `prd.md` (8 sections) + capability map → self-review.
- **Output:** `docs/specs/active/YYYY-MM-DD-<slug>/prd.md` (single feature) or `docs/ways-of-work/plan/{epic}/{feat}/prd.md` (multi-capability epic).
- **Gate:** STOP until user approves the refined concept. YAGNI — 2-3 options max.

### `/plan` — PLAN → `implementation-plan.md` + `todo.md`

- **Phase 1 (HOW):** reads `prd.md`, writes `implementation-plan.md` — 5-layer Mermaid (Frontend→API→Business→Data→Infra), DB schema/ERD, API spec (endpoints + TS types + auth), frontend hierarchy (shadcn/ui), security & perf.
- **Phase 2 (ORDER):** dependency graph + vertical slicing → `todo.md` / `tasks/plan.md` (tasks with Title, Description, AC, Verification, Dependencies, Files, Scope; checkpoints every 2-3 tasks).
- **Outputs:** `implementation-plan.md` alongside `prd.md` + `tasks/plan.md` + `tasks/todo.md` (always in `tasks/` or `docs/specs/active/<id>/` per project convention).

### `/build` — BUILD → code

- **Loop:** RED (failing test) → GREEN (minimal code) → regression (`test + build`) → conventional commit (`feat:`/`fix:`) → mark task done. Only stage files for the current task.
- **Auto:** `/build auto` generates `tasks/plan.md` if missing, then implements every task autonomously — still 1 commit per task, pauses on failure/risky step.

### `/verify` — VERIFY → green

- **Default:** run full `tests + build`; on failure follow `debugging-and-error-recovery` → 5-step triage + Prove-It guard test.
- **Conditional web:** `browser-testing-with-devtools` (DevTools) or `webapp-testing` (Playwright + `with_server.py`) — **only if the change touches browser/UI**; non-web projects skip entirely.
- **Conditional others:** `security-and-hardening` (input/auth), `performance-optimization` (N+1/CWV), `doubt-driven-development` (high stakes).
- **Gate:** do not proceed to `/review` while red.

### `/review` — REVIEW → report

- **Who:** `code-reviewer` persona (Senior Staff Engineer, 5-axis: correctness/readability/architecture/security/performance).
- **How:** invokes `code-review-and-quality` + `code-simplification` (incremental, 1 change at a time, tests green) + `documentation-and-adrs` (ADR in `docs/adr/`) + `deprecation-and-migration` (if needed).
- **Output:** structured report with Critical / Important / Suggestion + `file:line`. Critical must be fixed before `/ship`.

### `/ship` — SHIP → GO/NO-GO + archive

- **Orchestrator fan-out (parallel):**
  ```
  /ship
    ├── code-reviewer    → review report
    └── security-auditor → audit report (conditional — auth/input/deps)
                ↓ merge (main agent)
          GO / NO-GO + rollback plan (trigger + steps + RTO)
  ```
- **Checks:** `shipping-and-launch` pre-launch checklist, `ci-cd-and-automation`, `observability-and-instrumentation`, `git-workflow-and-versioning` (atomic commits, tags).
- **Archive gate:** moves `docs/specs/active/<id>` → `docs/specs/archive/<id>` only when all `todo.md` checkboxes are `[x]`; otherwise stays active.

## OPTIONAL — outside the per-feature lifecycle

### `/constraints` — SETUP (once)

- Runs `constraint-driven-development`: interviews (4 questions, one per message), tool detection (`tsc`, `eslint`, `gitleaks --redact`, `semgrep`, `osv-scanner`, `vitest --coverage`, `axe`, `lighthouse`), assigns checks by cost (`check:fast` <5s, `check:task` <90s, `check:full` in CI), watches diffs for weakened bars (new `@ts-ignore`, skipped tests, lowered thresholds), supports ratcheting.
- **Not per-feature** — run once at repo init or when the bar is undefined.

### `/explain-code` — READ-ONLY (anytime)

- **Three lenses (pick a/b/c, combinable):**
  - (a) `improve-codebase-architecture` — codebase architecture scan, deep-module opportunities, HTML report + Mermaid (choose Strong / Worth / Speculative).
  - (b) `database-schema-designer` — DB/data-model schema, ERD, checklist.
  - (c) `write-feature-docs` — feature documentation from existing code.
- **Does not modify code.** When done, suggest `/spec` if the user wants to act on findings.

## File format

Each command is `commands/<name>.toml`:

```toml
description = "SPEC — IDEA+PRD pipeline"
prompt = """
Invoke brainstorming first — hard-gate before any code ...
"""
```

The `prompt` is what the agent executes when the slash command is invoked.
