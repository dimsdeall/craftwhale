# AGENTS.md — craftwhale (dimsdeall)

Collection **30 Agent Skills + 8 Commands** — 6 CORE (Spec → Ship) + 2 OPTIONAL. Contract: `/constraints` (once, optional) → `/spec` → `prd.md` (WHAT/WHY) → `/plan` → `implementation-plan.md` (HOW) + `tasks/plan.md` (ORDER) → `/build` → code.

## Inventory (do not delete — source of truth)

- Define (5): `brainstorming`, `interview-me`, `idea-refine`, `spec-driven-development`, `constraint-driven-development`
- Plan (3): `planning-and-task-breakdown`, `context-engineering`, `using-agent-skills`
- Build (5): `incremental-implementation`, `test-driven-development`, `api-and-interface-design`, `frontend-ui-engineering`, `source-driven-development`
- Verify (6): `debugging-and-error-recovery`, `browser-testing-with-devtools`, `webapp-testing` (optional — web only, Playwright + with_server.py, Anthropic), `security-and-hardening`, `performance-optimization`, `doubt-driven-development`
- Review (4): `code-review-and-quality`, `code-simplification`, `documentation-and-adrs`, `deprecation-and-migration`
- Ship & Operate (4): `git-workflow-and-versioning`, `ci-cd-and-automation`, `shipping-and-launch`, `observability-and-instrumentation`
- Explain (3, optional — read-only): `improve-codebase-architecture` (mattpocock/skills), `database-schema-designer` (softaworks/agent-toolkit), `write-feature-docs` (warpdotdev/common-skills)
- Shared `references/`: 7 checklists (accessibility, definition-of-done, observability, orchestration, performance, security, testing)
- Commands `commands/*.toml` (8): **CORE 6** `/spec` → `brainstorming+idea-refine+interview-me+spec-driven` → `prd.md` (WHAT/WHY, 8-section PRD), `/plan` → `planning+context+api/database` → `implementation-plan.md` (HOW, 5-layer Mermaid + DB ERD + API + frontend) + `tasks/plan.md` (ORDER, vertical slices), `/build` → `incremental+TDD`, `/verify` → `debugging+security/perf/doubt+webapp-testing` (web optional — skip if not web), `/review` → `code-review+code-simplification+ADRs`, `/ship` → `shipping+CI/CD+observability+git` — **OPTIONAL 2** `/constraints` → `constraint-driven` (interview 4Q → CONSTRAINTS.md), `/explain-code` → `improve-codebase-architecture+database-schema-designer+write-feature-docs` (a/b/c, read-only)

## Rules for AI agents working on this repo

- Each skill = `skills/<name>/SKILL.md` with valid `name` + `description` frontmatter. `name` must equal folder name (lowercase, hyphen).
- `brainstorming` is the **first gate** before any other skill — classifies Spike/Bounded/Architectural + hard-gate approval before coding. Do not skip.
- Shared checklists in `references/` — reference via relative path from the skill.
- New skill: duplicate the nearest skill as template → edit frontmatter → push.
- After adding/editing a skill → test: `npx skills add dimsdeall/craftwhale --list` should show (`Found 30 skills`).

## Intent → Skill Mapping (for agents using this repo via `npx skills add dimsdeall/craftwhale`)

- Don't know what to build / rough idea → `brainstorming` first, then `interview-me` / `idea-refine`
- Want a spec/PRD → `spec-driven-development`
- Have a spec, want to break it into tasks → `planning-and-task-breakdown`
- Need repo context → `context-engineering` / `source-driven-development`
- Writing code → `incremental-implementation` + `test-driven-development` (+ `api-and-interface-design` / `frontend-ui-engineering` if relevant)
- Web verification (optional — only for webapp/UI) → `webapp-testing` (Playwright + with_server.py) or `browser-testing-with-devtools` — skip if not web
- Bug / error → `debugging-and-error-recovery` (+ `doubt-driven-development` if high stakes)
- Review → `code-review-and-quality` → `code-simplification` if needed
- Commit/PR → `git-workflow-and-versioning`
- CI/CD, release, monitoring → `ci-cd-and-automation`, `shipping-and-launch`, `observability-and-instrumentation`
- Want to explain architecture/schema/feature (read-only) → `/explain-code` → `improve-codebase-architecture` / `database-schema-designer` / `write-feature-docs`
- Want a quality bar → `/constraints` → `constraint-driven-development`

## Provenance

- 25 skills from `addyosmani/agent-skills` (MIT)
- 1 skill `brainstorming` from `obra/superpowers` (MIT, S-rank)
- 1 skill `improve-codebase-architecture` from `mattpocock/skills` (MIT, 915K)
- 1 skill `database-schema-designer` from `softaworks/agent-toolkit` (MIT)
- 1 skill `write-feature-docs` from `warpdotdev/common-skills` (MIT)
- 1 skill `webapp-testing` from `anthropics/skills` (MIT, Playwright + with_server.py)
