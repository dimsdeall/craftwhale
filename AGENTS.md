# AGENTS.md — my-skills (dimsdeall)

Koleksi **29 Agent Skills** — lifecycle Idea → Ship + workflow khusus Dimas.

## Inventory (jangan hapus — source of truth)

- Custom (3): `hello-world`, `hermes-workflow`, `9router-ops`
- Define (5): `brainstorming`, `interview-me`, `idea-refine`, `spec-driven-development`, `constraint-driven-development`
- Plan (3): `planning-and-task-breakdown`, `context-engineering`, `using-agent-skills`
- Build (5): `incremental-implementation`, `test-driven-development`, `api-and-interface-design`, `frontend-ui-engineering`, `source-driven-development`
- Verify (5): `debugging-and-error-recovery`, `browser-testing-with-devtools`, `security-and-hardening`, `performance-optimization`, `doubt-driven-development`
- Review (4): `code-review-and-quality`, `code-simplification`, `documentation-and-adrs`, `deprecation-and-migration`
- Ship & Operate (4): `git-workflow-and-versioning`, `ci-cd-and-automation`, `shipping-and-launch`, `observability-and-instrumentation`
- Shared `references/`: 7 checklist (accessibility, definition-of-done, observability, orchestration, performance, security, testing)

## Aturan untuk AI agent yang ngerjain repo ini

- Tiap skill = `skills/<name>/SKILL.md` dengan frontmatter `name` + `description` valid. `name` == nama folder (lowercase, hyphen).
- `brainstorming` adalah **gerbang pertama** sebelum semua skill lain — klasifikasi Spike/Bounded/Architectural + hard-gate approval sebelum coding. Jangan skip.
- Jangan copy `AGENTS.md` dari repo lain — ini sudah file repo sendiri.
- Shared checklist di `references/` — referensikan via path relatif dari skill.
- Skill baru: `cp -r skills/hello-world skills/<baru>` → edit frontmatter → push.
- Setelah tambah/edit skill → test: `npx skills add dimsdeall/my-skills --list` harus muncul (private → butuh gh auth dimsdeall).

## Intent → Skill Mapping (untuk agent yang pakai repo ini via `npx skills add dimsdeall/my-skills`)

- Belum tahu mau bikin apa / ide kasar → `brainstorming` dulu, lalu `interview-me` / `idea-refine`
- Mau spec/PRD → `spec-driven-development`
- Ada spec, mau pecah task → `planning-and-task-breakdown`
- Butuh konteks repo → `context-engineering` / `source-driven-development`
- Nulis kode → `incremental-implementation` + `test-driven-development` (+ `api-and-interface-design` / `frontend-ui-engineering` bila relevan)
- Bug / error → `debugging-and-error-recovery` (+ `doubt-driven-development` bila stakes tinggi)
- Review → `code-review-and-quality` → `code-simplification` bila perlu
- Commit/PR → `git-workflow-and-versioning`
- CI/CD, rilis, monitor → `ci-cd-and-automation`, `shipping-and-launch`, `observability-and-instrumentation`
- Kerja di Hermes/9Router → `hermes-workflow` / `9router-ops`

## Provenance

- 25 skills dari `addyosmani/agent-skills` (MIT)
- 1 skill `brainstorming` dari `obra/superpowers` (MIT, S-rank)
- 3 custom milik dimsdeall
- Semua skill ter-copy utuh (termasuk scripts/references per-skill bila ada).
