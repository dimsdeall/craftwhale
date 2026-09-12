# AGENTS.md — my-skills (dimsdeall)

Repo ini adalah **koleksi Agent Skills** milik Dimas. Skill ada di `skills/<name>/SKILL.md`.

## Aturan untuk AI agent yang ngerjain repo ini

- Skill baru = folder baru di `skills/<nama>/SKILL.md` dengan frontmatter `name` + `description` yang valid. `name` harus sama dengan nama folder (lowercase, hyphen).
- Jangan copy `AGENTS.md` dari addyosmani/agent-skills — ini sudah file repo sendiri.
- Tiap SKILL.md harus punya: Overview, When to Use, Workflow (numbered steps), dan contoh command bila relevan.
- Shared checklist taruh di `references/` dan referensikan dari skill via path relatif.
- Setelah tambah/edit skill → test instal: `npx skills add dimsdeall/my-skills --list` harus muncul.

## Intent → Skill Mapping (untuk agent yang pakai repo ini)

- Tes instalasi / template → `hello-world`
- Kerja di Hermes TUI / cron / Combi-hermes → `hermes-workflow`
- Update/debug 9Router (PM2/build) → `9router-ops`
