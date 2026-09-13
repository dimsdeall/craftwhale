# Lifecycle — Idea → Ship

> Source of truth for how work flows through this repo.

```
/constraints (optional, once — quality bar)
    │
┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐
│ IDEA │ ───▶ │ SPEC │ ───▶ │ PLAN │ ───▶ │BUILD │ ───▶ │VERIFY│ ───▶ │REVIEW│ ───▶ │ SHIP │
│Brain │      │ PRD  │      │ HOW  │      │ Code │      │ Test │      │ Gate │      │  Go  │
└──────┘      └──────┘      └──────┘      └──────┘      └──────┘      └──────┘      └──────┘
 /spec         /spec         /plan         /build       /verify       /review        /ship  
```

## Contract per Phase

| Phase | Command | Input | Output | Approval Gate |
|-------|---------|-------|--------|---------------|
| Constraints | `/constraints` | Repo context (package.json, linters, coverage) | `docs/CONSTRAINTS.md` | Interview 4Q → committed file |
| Spec | `/spec` | Idea + context + interview | `docs/specs/active/<spec-id>/prd.md` | Present concept → **STOP, wait for explicit approval** → write PRD → review |
| Plan | `/plan` | Approved `prd.md` | `docs/specs/active/<spec-id>/implementation-plan.md` + `todo.md` | Present both → wait for approval |
| Build | `/build` / `/build auto` | `todo.md` | Code + tests + commits | 1 task = 1 commit, RED→GREEN→regression→build |
| Verify | `/verify` | Code for `<spec-id>` | Green tests/build + guard tests | **Do not proceed to /review while red** |
| Review | `/review` | Diff for `<spec-id>` | 5-axis report + ADRs (if any) | Fix Critical before /ship |
| Ship | `/ship` | Green VERIFY+REVIEW | Tag + CHANGELOG + archive (`docs/specs/archive/`) | GO/NO-GO + rollback plan |

## Detailed Flow

1. **/constraints** — once at repo start (optional). Detects stack, interviews max 4 questions, writes `docs/CONSTRAINTS.md` (Floor + Enforced with numbers + Measured + Exceptions), wires checks by cost (BUILD <5s, VERIFY <90s, REVIEW minutes, SHIP CI).

2. **/spec → prd.md (WHAT & WHY)** — hard-gate `brainstorming` (Spike/Bounded/Architectural) → `idea-refine` → `interview-me` (~95% confidence) → present refined concept → approval → write 8-section PRD (Feature Name, Epic, Goal Problem/Solution/Impact, Personas, User Stories, Func+NFunc Requirements, Acceptance Criteria Given/When/Then, Out of Scope) → self-review → commit.

3. **/plan → implementation-plan.md (HOW) + todo.md (ORDER)** — reads approved `prd.md`, enter plan mode (read-only), writes `implementation-plan.md` (Mermaid 5-layer architecture: Frontend→API→Business→Data→Infra, DB ERD, API spec with TS types, Frontend hierarchy, Security/Perf) then vertical slices → `todo.md` (Title, Description, AC, Verification, Dependencies, Files, Scope) with checkpoints every 2-3 tasks.

4. **/build → code** — resolves active `<spec-id>`, picks next unchecked task, RED (failing test) → GREEN (minimal code) → regression (full suite + build) → conventional commit + mark `[x]` in `todo.md`. `/build auto` loops over all todos after one plan approval.

5. **/verify → green** — full tests+build, `debugging-and-error-recovery` if red (Prove-It: reproduce→localize→fix→guard test→re-verify), scoped to files touched by that spec. Conditional: `webapp-testing`/`browser-testing-with-devtools` (only if web/UI), `security-and-hardening` (input/auth), `performance-optimization` (N+1/CWV), `doubt-driven-development` (high stakes).

6. **/review → report** — via `code-reviewer` persona (5 axes), categorized Critical/Important/Suggestion with `file:line`, `code-simplification` if complex, ADR in `docs/adr/` if needed. Critical must be fixed before `/ship`.

7. **/ship → GO/NO-GO** — fan-out `code-reviewer` + `security-auditor` (conditional) in parallel → merge → pre-launch checklist → GO/NO-GO + rollback plan (trigger+steps+RTO). Archive gate moves `docs/specs/active/<id>` → `docs/specs/archive/<id>` only if all todos are `[x]`.

## Optional vs Core

- **Core** (every feature): `/spec` → `/plan` → `/build` → `/verify` → `/review` → `/ship`
- **Optional** (outside core, still slash commands): `/constraints` (setup once), `/explain-code` (read-only, anytime)
