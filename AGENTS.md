# AGENTS.md — craftwhale 🐋 (dimsdeall)

Koleksi **30 Agent Skills + 8 Commands** — 6 CORE (Spec → Ship) + 2 OPSIONAL. Kontrak: /constraints (sekali, opsional) → /spec → prd.md (WHAT/WHY) → /plan → implementation-plan.md (HOW) + tasks/plan.md (ORDER) → /build → code.

## Inventory (jangan hapus — source of truth)

- Define (5): `brainstorming`, `interview-me`, `idea-refine`, `spec-driven-development`, `constraint-driven-development`
- Plan (3): `planning-and-task-breakdown`, `context-engineering`, `using-agent-skills`
- Build (5): `incremental-implementation`, `test-driven-development`, `api-and-interface-design`, `frontend-ui-engineering`, `source-driven-development`
- Verify (6): `debugging-and-error-recovery`, `browser-testing-with-devtools`, `webapp-testing` (opsional — hanya web, Playwright + with_server.py, Anthropic), `security-and-hardening`, `performance-optimization`, `doubt-driven-development`
- Review (4): `code-review-and-quality`, `code-simplification`, `documentation-and-adrs`, `deprecation-and-migration`
- Ship & Operate (4): `git-workflow-and-versioning`, `ci-cd-and-automation`, `shipping-and-launch`, `observability-and-instrumentation`
- Explain (3, opsional — read-only): `improve-codebase-architecture` (mattpocock/skills), `database-schema-designer` (softaworks/agent-toolkit), `write-feature-docs` (warpdotdev/common-skills)
- Shared `references/`: 7 checklist (accessibility, definition-of-done, observability, orchestration, performance, security, testing)
- Commands `commands/*.toml` (8): **CORE 6** `/spec` → `brainstorming+idea-refine+interview-me+spec-driven` → `prd.md` (WHAT/WHY, 8-section PRD), `/plan` → `planning+context+api/database` → `implementation-plan.md` (HOW, 5-layer Mermaid + DB ERD + API + frontend) + `tasks/plan.md` (ORDER, vertical slices), `/build` → `incremental+TDD`, `/verify` → `debugging+security/perf/doubt+webapp-testing` (web opsional — skip bila bukan web), `/review` → `code-review+code-simplification+ADRs`, `/ship` → `shipping+CI/CD+observability+git` — **OPSIONAL 2** `/constraints` → `constraint-driven` (interview 4Q → CONSTRAINTS.md), `/explain-code` → `improve-codebase-architecture+database-schema-designer+write-feature-docs` (a/b/c, read-only)

## Aturan untuk AI agent yang ngerjain repo ini

- Tiap skill = `skills/<name>/SKILL.md` dengan frontmatter `name` + `description` valid. `name` == nama folder (lowercase, hyphen).
- `brainstorming` adalah **gerbang pertama** sebelum semua skill lain — klasifikasi Spike/Bounded/Architectural + hard-gate approval sebelum coding. Jangan skip.
- Shared checklist di `references/` — referensikan via path relatif dari skill.
- Skill baru: duplikasi skill terdekat sebagai template → edit frontmatter → push.
- Setelah tambah/edit skill → test: `npx skills add dimsdeall/craftwhale --list` harus muncul (`Found 30 skills`).

## Intent → Skill Mapping (untuk agent yang pakai repo ini via `npx skills add dimsdeall/craftwhale`)

- Belum tahu mau bikin apa / ide kasar → `brainstorming` dulu, lalu `interview-me` / `idea-refine`
- Mau spec/PRD → `spec-driven-development`
- Ada spec, mau pecah task → `planning-and-task-breakdown`
- Butuh konteks repo → `context-engineering` / `source-driven-development`
- Nulis kode → `incremental-implementation` + `test-driven-development` (+ `api-and-interface-design` / `frontend-ui-engineering` bila relevan)
- Verifikasi web (opsional — hanya bila webapp/UI) → `webapp-testing` (Playwright + with_server.py) atau `browser-testing-with-devtools` — skip bila bukan web
- Bug / error → `debugging-and-error-recovery` (+ `doubt-driven-development` bila stakes tinggi)
- Review → `code-review-and-quality` → `code-simplification` bila perlu
- Commit/PR → `git-workflow-and-versioning`
- CI/CD, rilis, monitor → `ci-cd-and-automation`, `shipping-and-launch`, `observability-and-instrumentation`
- Mau jelaskan arsitektur/skema/fitur (read-only) → `/explain-code` → `improve-codebase-architecture` / `database-schema-designer` / `write-feature-docs`
- Mau quality bar → `/constraints` → `constraint-driven-development`

## Provenance

- 25 skills dari `addyosmani/agent-skills` (MIT)
- 1 skill `brainstorming` dari `obra/superpowers` (MIT, S-rank)
- 1 skill `improve-codebase-architecture` dari `mattpocock/skills` (MIT, 915K)
- 1 skill `database-schema-designer` dari `softaworks/agent-toolkit` (MIT)
- 1 skill `write-feature-docs` dari `warpdotdev/common-skills` (MIT)
- 1 skill `webapp-testing` dari `anthropics/skills` (MIT, Playwright + with_server.py)
