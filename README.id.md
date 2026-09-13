# craftwhale

> *Membangun kapal besar untuk lautan, didampingi paus.*

> [English](README.md) | **Indonesia**

Kumpulan agent skills production-grade — lifecycle lengkap **Idea → Ship**. **30 skills + 2 persona + 8 slash command**, dikurasi dari sumber terbuka dan dirangkai dalam satu kontrak.

Kompatibel dengan 70+ agent (Claude Code, Cursor, Codex, Copilot, Cline, OpenCode, Hermes, dll.) via CLI open `skills`.

## Cara Kerja

Setiap fitur lewat kontrak yang sama. Satu spec = satu folder, tidak ada yang rilis tanpa lewat gate-nya. `Command = WHEN` · `Skill = HOW` · `Persona = WHO`.

```
/constraints (opsional, sekali — quality bar)
    │
┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐
│ SPEC │ ───▶ │ PLAN │ ───▶ │BUILD │ ───▶ │VERIFY│ ───▶ │REVIEW│ ───▶ │ SHIP │
│I/PRD │      │ HOW  │      │ Code │      │ Test │      │ Gate │      │  Go  │
└──────┘      └──────┘      └──────┘      └──────┘      └──────┘      └──────┘
 /spec         /plan         /build       /verify       /review        /ship  
```

| Fase | Command (WHEN) | Skills (HOW) | Output |
|------|----------------|--------------|--------|
| **Constraints** *(sekali, opsional)* | `/constraints` | `constraint-driven-development` — interview 4Q → Floor + Enforced + Exceptions | `docs/CONSTRAINTS.md` + `check:fast/task/full` |
| **Spec** | `/spec` | `brainstorming` (hard-gate) · `interview-me` · `idea-refine` · `spec-driven-development` | `docs/specs/active/<id>/prd.md` (8 section: Goal, Persona, Stories, Requirements, AC) — **STOP tunggu approval** |
| **Plan** | `/plan` | `planning-and-task-breakdown` · `context-engineering` · `using-agent-skills` | `implementation-plan.md` (Mermaid 5-layer + ERD + API + frontend) + `todo.md` (vertical slices) — approval |
| **Build** | `/build` | `incremental-implementation` · `test-driven-development` · `api-and-interface-design` · `frontend-ui-engineering` · `source-driven-development` | code + tests — 1 task = 1 commit `RED→GREEN→regression` |
| **Verify** | `/verify` | `debugging-and-error-recovery` · `browser-testing-with-devtools` · `webapp-testing` *(web opsional)* · `security-and-hardening` · `performance-optimization` · `doubt-driven-development` | tests + build hijau — harus hijau sebelum review |
| **Review** | `/review` | `code-review-and-quality` · `code-simplification` · `documentation-and-adrs` · `deprecation-and-migration` + persona `code-reviewer` (5-axis) | laporan `Critical/Important/Suggestion` + `file:line` + ADR — fix Critical sebelum ship |
| **Ship** | `/ship` | `git-workflow-and-versioning` · `ci-cd-and-automation` · `shipping-and-launch` · `observability-and-instrumentation` + `code-reviewer` + `security-auditor` fan-out | tag · CHANGELOG · `docs/specs/archive/<id>/` (hanya bila todo 100% ✔) — GO/NO-GO + rollback |
| **Explain** *(kapan saja, opsional, read-only)* | `/explain-code` | `improve-codebase-architecture` · `database-schema-designer` · `write-feature-docs` | `docs/explain/` — arsitektur / skema / fitur |

> **30 skills** dikelompokkan di atas + `references/` ×7 checklist bersama. Tabel lengkap, provenance & install per kategori (Define/Plan/Build/Verify/Review/Ship/Explain/Personas) → [docs/skills.md](docs/skills.md) · [docs/personas.md](docs/personas.md) · [docs/commands.md](docs/commands.md) · [docs/installation.md](docs/installation.md) · gate lifecycle → [docs/lifecycle.md](docs/lifecycle.md)

## Persona (2 — opsional, WHO)

| Persona | Peran | Dipakai di |
|---------|-------|------------|
| `code-reviewer` | Senior Staff Engineer — review 5-axis (correctness/readability/architecture/security/perf) | `/review` · `/ship` fan-out |
| `security-auditor` | Security Engineer — OWASP & threat modeling, hanya isu yang exploitable | `/ship` fan-out (kondisional — hanya bila spec sentuh auth/input) |

Persona tidak memanggil persona lain — komposisi ada di command. Detail → [docs/personas.md](docs/personas.md)

## Struktur Development

**Repo ini (`craftwhale`)** — library skill-nya sendiri:

```
craftwhale/
├── agents/*.md          # 2 persona (WHO)
├── commands/*.toml      # 8 slash commands (WHEN)
├── skills/<name>/       # 30 skills (HOW)
├── references/          # 7 shared checklist
├── docs/                # docs teknis (lifecycle, skills, personas, commands, dst.)
└── README.md / README.id.md
```

**Project consumer** (tempat Kak jalankan `/spec` → `/ship`) — semua artefak ada di `docs/`:

```
project-root/
└── docs/
    ├── CONSTRAINTS.md                 # dari /constraints (sekali)
    ├── specs/
    │   ├── active/YYYY-MM-DD-<slug>/  # /spec bikin 1 folder per spec
    │   │   ├── prd.md                 # WHAT & WHY
    │   │   ├── implementation-plan.md # HOW
    │   │   └── todo.md                # ORDER
    │   └── archive/<slug>/            # /ship pindah ke sini hanya bila todo 100%
    ├── adr/                           # dari /review
    └── explain/                       # dari /explain-code (hanya bila diminta)
```

Aturan: spec baru = folder baru di `active/`; collision (overlap file/module) → tanya **Gabung / Pisah / Tunda**; archive hanya via `/ship` bila semua `- [ ]` → `- [x]`. Layout lengkap & aturan → [docs/structure.md](docs/structure.md)

## Docs

| Halaman | Isinya |
|---------|--------|
| [docs/lifecycle.md](docs/lifecycle.md) | Alur Idea → Ship & gate |
| [docs/commands.md](docs/commands.md) | 8 slash commands — input, output, gate |
| [docs/personas.md](docs/personas.md) | 2 persona — peran & komposisi |
| [docs/skills.md](docs/skills.md) | 30 skills — per kelompok + provenance |
| [docs/structure.md](docs/structure.md) | Layout file repo ini & project consumer |
| [docs/constraints.md](docs/constraints.md) | Quality bar (`docs/CONSTRAINTS.md`) |
| [docs/explaining.md](docs/explaining.md) | `/explain-code` — 3 lensa read-only |
| [docs/installation.md](docs/installation.md) | Instal, update, local copy |

Index lengkap → [docs/README.md](docs/README.md)

## Lisensi

MIT — bebas pakai dan modifikasi.
