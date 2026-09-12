# my-skills — Dimas Putra (dimsdeall)

> [English](README.md) | **Indonesia**

Kumpulan agent skills production-grade — lifecycle lengkap **Idea → Ship**. 30 skills + 2 persona + 8 slash command, dikurasi dari sumber terbuka dan dirangkai dalam satu kontrak.

## Instalasi

Repo ini **private** — jalankan `gh auth login` sebagai `dimsdeall` atau minta akses sebagai collaborator. Kompatibel dengan 70+ agent (Claude Code, Cursor, Codex, Copilot, Cline, OpenCode, Hermes, dll.) via CLI open `skills`.

```bash
# lihat dulu
npx skills add dimsdeall/my-skills --list

# pasang semua (30 skills + 8 commands + 2 personas)
npx skills add dimsdeall/my-skills

# atau satu skill
npx skills add dimsdeall/my-skills --skill brainstorming
```

Update & instal manual → [docs/installation.md](docs/installation.md)

## Lifecycle

```
/constraints (opsional, sekali)
    │
IDEA ──→ SPEC ──→ PLAN ──→ BUILD ──→ VERIFY ──→ REVIEW ──→ SHIP ──→ OPERATE
```

- `/constraints` sekali → `/spec` → `prd.md` (WHAT & WHY) → `/plan` → `implementation-plan.md` (HOW) + `todo.md` (ORDER) → `/build` → code → `/verify` → hijau → `/review` → laporan → `/ship` → GO/NO-GO + archive.

Detail → [docs/lifecycle.md](docs/lifecycle.md)

## Skills (30)

Dikurasi dari `addyosmani/agent-skills` (25), `obra/superpowers — brainstorming` (1), `mattpocock/skills` (1), `softaworks/agent-toolkit` (1), `warpdotdev/common-skills` (1), dan `anthropics/skills` (1).

| Kelompok | Jumlah | Docs |
|----------|--------|------|
| Define | 5 | [docs/skills.md](docs/skills.md) |
| Plan | 3 | |
| Build | 5 | |
| Verify | 6 (web opsional) | |
| Review | 4 | |
| Ship & Operate | 4 | |
| Explain (read-only, opsional) | 3 | |

Tabel lengkap + sumber → [docs/skills.md](docs/skills.md) · Checklist bersama ada di `references/` (7).

## Persona (2 — opsional)

| Persona | Peran | Dipakai di |
|---------|-------|------------|
| `code-reviewer` | Senior Staff Engineer — review 5-axis | `/review` · `/ship` fan-out |
| `security-auditor` | Security Engineer — OWASP & threat modeling | `/ship` fan-out (kondisional) |

`Skill = HOW` · `Persona = WHO` · `Command = WHEN` → [docs/personas.md](docs/personas.md)

## Commands (8 = 6 CORE + 2 OPTIONAL)

| Command | Fase | Output |
|---------|------|--------|
| `/spec` | SPEC | `docs/specs/active/<id>/prd.md` |
| `/plan` | PLAN | `implementation-plan.md` + `todo.md` |
| `/build` | BUILD | code + tests (1 commit per task) |
| `/verify` | VERIFY | gate hijau |
| `/review` | REVIEW | laporan `code-reviewer` + ADR |
| `/ship` | SHIP | tag · CHANGELOG · `docs/specs/archive/` |
| `/constraints` | *opsional* | `docs/CONSTRAINTS.md` |
| `/explain-code` | *opsional, read-only* | arsitektur / skema / fitur |

Kontrak per command → [docs/commands.md](docs/commands.md)

## Struktur

Semua output ada di `docs/` — per folder spec `docs/specs/active/YYYY-MM-DD-<slug>/` → `docs/specs/archive/` saat `/ship` bila todo 100%. Detail → [docs/structure.md](docs/structure.md)

## Docs

| Halaman | Isinya |
|---------|--------|
| [docs/lifecycle.md](docs/lifecycle.md) | Alur end-to-end & gate |
| [docs/skills.md](docs/skills.md) | 30 skills |
| [docs/personas.md](docs/personas.md) | 2 persona (WHO) |
| [docs/commands.md](docs/commands.md) | 8 commands (WHEN) |
| [docs/structure.md](docs/structure.md) | Layout file & aturan collision/archive |
| [docs/constraints.md](docs/constraints.md) | Quality bar (`docs/CONSTRAINTS.md`) |
| [docs/explaining.md](docs/explaining.md) | Lensa `/explain-code` |
| [docs/installation.md](docs/installation.md) | Instal & update |

## Lisensi

MIT — bebas pakai dan modifikasi.
