# Skills — 30 Total

> All skills live in `skills/<name>/SKILL.md`. One folder = one `SKILL.md` (required name == folder).

## Define — What to Build (5)

| Skill | Description | Source |
|-------|-------------|--------|
| `brainstorming` | **First gate** — classify Spike/Bounded/Architectural, Socratic refinement, hard-gate approval before coding (S-rank) | `obra/superpowers` |
| `interview-me` | One-question-at-a-time requirements interrogation | `addyosmani/agent-skills` |
| `idea-refine` | Divergent/convergent idea exploration | `addyosmani/agent-skills` |
| `spec-driven-development` | Write spec/PRD before coding — single source of truth | `addyosmani/agent-skills` |
| `constraint-driven-development` | Define quality bar once, enforce everywhere → `docs/CONSTRAINTS.md` | `addyosmani/agent-skills` |

## Plan — How to Break It Down (3)

| Skill | Description | Source |
|-------|-------------|--------|
| `planning-and-task-breakdown` | Decompose spec into atomic tasks with AC | `addyosmani/agent-skills` |
| `context-engineering` | Prepare repo context: structure, existing patterns | `addyosmani/agent-skills` |
| `using-agent-skills` | Meta-skill — route intent → right skill | `addyosmani/agent-skills` |

## Build — Writing Code (5)

| Skill | Description | Source |
|-------|-------------|--------|
| `incremental-implementation` | One slice one commit, no big bang | `addyosmani/agent-skills` |
| `test-driven-development` | RED-GREEN-REFACTOR, 80%+ coverage | `addyosmani/agent-skills` |
| `api-and-interface-design` | Contract-first API & interface design | `addyosmani/agent-skills` |
| `frontend-ui-engineering` | Component architecture, design systems, state | `addyosmani/agent-skills` |
| `source-driven-development` | Ground decisions in official docs — verify & cite | `addyosmani/agent-skills` |

## Verify — Prove It Works (6, web optional)

| Skill | Description | Source |
|-------|-------------|--------|
| `debugging-and-error-recovery` | Reproduce → localize → fix → guard | `addyosmani/agent-skills` |
| `browser-testing-with-devtools` | Browser automation via Chrome DevTools | `addyosmani/agent-skills` |
| `webapp-testing` | **Optional — web only** — Playwright + `with_server.py`, screenshots & console logs | `anthropics/skills` |
| `security-and-hardening` | OWASP Top 10, auth, secrets, supply chain | `addyosmani/agent-skills` |
| `performance-optimization` | Measure-first, Core Web Vitals, profiling | `addyosmani/agent-skills` |
| `doubt-driven-development` | Adversarial review for high-stakes / unfamiliar code | `addyosmani/agent-skills` |

> Web verification is optional — skip for CLI, library, API-only, or cron projects.

## Review — Should We Merge? (4)

| Skill | Description | Source |
|-------|-------------|--------|
| `code-review-and-quality` | 5-axis review: correctness, design, readability, test, security | `addyosmani/agent-skills` |
| `code-simplification` | Clarity over cleverness | `addyosmani/agent-skills` |
| `documentation-and-adrs` | ADRs & architectural decision docs | `addyosmani/agent-skills` |
| `deprecation-and-migration` | Safe deprecation & migration | `addyosmani/agent-skills` |

## Ship & Operate (4)

| Skill | Description | Source |
|-------|-------------|--------|
| `git-workflow-and-versioning` | Branching, conventional commits, PR hygiene | `addyosmani/agent-skills` |
| `ci-cd-and-automation` | CI/CD pipelines | `addyosmani/agent-skills` |
| `shipping-and-launch` | Release checklist & go-live | `addyosmani/agent-skills` |
| `observability-and-instrumentation` | Logging, metrics, tracing, alerting | `addyosmani/agent-skills` |

## Explain — Read-Only, Optional (3)

| Skill | Description | Source |
|-------|-------------|--------|
| `improve-codebase-architecture` | Scan architecture, deep-module opportunities, HTML report + Mermaid (915K) | `mattpocock/skills` |
| `database-schema-designer` | Design & explain DB/data-model schema, ERD, checklist | `softaworks/agent-toolkit` |
| `write-feature-docs` | Feature docs from an existing codebase | `warpdotdev/common-skills` |

## Shared References (7)

Pack-level checklists in `references/` used by multiple skills. Per-skill `npx` install copies only `skills/<name>/` — whole-repo install or manual copy is needed for these.

- `accessibility-checklist.md`
- `definition-of-done.md`
- `observability-checklist.md`
- `orchestration-patterns.md`
- `performance-checklist.md`
- `security-checklist.md`
- `testing-patterns.md`

## Provenance

- 25 from `addyosmani/agent-skills`
- 1 `brainstorming` from `obra/superpowers` (MIT, S-rank)
- 1 `improve-codebase-architecture` from `mattpocock/skills` (MIT)
- 1 `database-schema-designer` from `softaworks/agent-toolkit` (MIT)
- 1 `write-feature-docs` from `warpdotdev/common-skills` (MIT)
- 1 `webapp-testing` from `anthropics/skills` (MIT)
