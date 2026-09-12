# my-skills — Dimas Putra (dimsdeall)

> **English** | [Indonesia](README.id.md)

Production-grade agent skills — a full **Idea → Ship** lifecycle. 30 skills + 2 personas + 8 slash commands, curated from open sources and wired to work together under one contract.

## Install

This repo is **private** — run `gh auth login` as `dimsdeall` or be added as collaborator. Works with 70+ agents (Claude Code, Cursor, Codex, Copilot, Cline, OpenCode, Hermes, etc.) via the open `skills` CLI.

```bash
# browse first
npx skills add dimsdeall/my-skills --list

# install everything (30 skills + 8 commands + 2 personas)
npx skills add dimsdeall/my-skills

# or one skill
npx skills add dimsdeall/my-skills --skill brainstorming
```

Updating & manual install → [docs/installation.md](docs/installation.md)

## Lifecycle

```
/constraints (optional, once)
    │
IDEA ──→ SPEC ──→ PLAN ──→ BUILD ──→ VERIFY ──→ REVIEW ──→ SHIP ──→ OPERATE
```

- `/constraints` once → `/spec` → `prd.md` (WHAT & WHY) → `/plan` → `implementation-plan.md` (HOW) + `todo.md` (ORDER) → `/build` → code → `/verify` → green → `/review` → report → `/ship` → GO/NO-GO + archive.

Details → [docs/lifecycle.md](docs/lifecycle.md)

## Skills (30)

Curated from `addyosmani/agent-skills` (25), `obra/superpowers — brainstorming` (1), `mattpocock/skills` (1), `softaworks/agent-toolkit` (1), `warpdotdev/common-skills` (1), and `anthropics/skills` (1).

| Group | Count | Docs |
|-------|-------|------|
| Define | 5 | [docs/skills.md#Define](docs/skills.md) |
| Plan | 3 | |
| Build | 5 | |
| Verify | 6 (web optional) | |
| Review | 4 | |
| Ship & Operate | 4 | |
| Explain (read-only, optional) | 3 | |

Full table + sources → [docs/skills.md](docs/skills.md) · Shared checklists live in `references/` (7).

## Personas (2 — optional)

| Persona | Role | Used in |
|---------|------|---------|
| `code-reviewer` | Senior Staff Engineer — 5-axis review | `/review` · `/ship` fan-out |
| `security-auditor` | Security Engineer — OWASP & threat modeling | `/ship` fan-out (conditional) |

`Skill = HOW` · `Persona = WHO` · `Command = WHEN` → [docs/personas.md](docs/personas.md)

## Commands (8 = 6 CORE + 2 OPTIONAL)

| Command | Phase | Output |
|---------|-------|--------|
| `/spec` | SPEC | `docs/specs/active/<id>/prd.md` |
| `/plan` | PLAN | `implementation-plan.md` + `todo.md` |
| `/build` | BUILD | code + tests (1 commit per task) |
| `/verify` | VERIFY | green gates |
| `/review` | REVIEW | `code-reviewer` report + ADR |
| `/ship` | SHIP | tag · CHANGELOG · `docs/specs/archive/` |
| `/constraints` | *optional* | `docs/CONSTRAINTS.md` |
| `/explain-code` | *optional, read-only* | architecture / schema / features |

Full contract per command → [docs/commands.md](docs/commands.md)

## Structure

All outputs live under `docs/` — per-spec folders `docs/specs/active/YYYY-MM-DD-<slug>/` → `docs/specs/archive/` on `/ship` when todos hit 100%. Details → [docs/structure.md](docs/structure.md)

## Docs

| Page | What |
|------|------|
| [docs/lifecycle.md](docs/lifecycle.md) | End-to-end flow & gates |
| [docs/skills.md](docs/skills.md) | All 30 skills |
| [docs/personas.md](docs/personas.md) | 2 personas (WHO) |
| [docs/commands.md](docs/commands.md) | 8 commands (WHEN) |
| [docs/structure.md](docs/structure.md) | File layout & collision/archive rules |
| [docs/constraints.md](docs/constraints.md) | Quality bar (`docs/CONSTRAINTS.md`) |
| [docs/explaining.md](docs/explaining.md) | `/explain-code` lenses |
| [docs/installation.md](docs/installation.md) | Install & update |

## License

MIT — free to use and modify.
