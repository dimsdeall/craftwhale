# my-skills — Dimas Putra (dimsdeall)

> [English](README.md) | **Indonesia**

Kumpulan agent skills production-grade — lifecycle lengkap **Idea → Ship**. **30 skills + 2 persona + 8 slash command**, dikurasi dari sumber terbuka dan dirangkai dalam satu kontrak.

Kompatibel dengan 70+ agent (Claude Code, Cursor, Codex, Copilot, Cline, OpenCode, Hermes, dll.) via CLI open `skills`. Repo ini **private** — `gh auth login` sebagai `dimsdeall` atau minta akses sebagai collaborator.

## Instalasi

```bash
# lihat dulu
npx skills add dimsdeall/my-skills --list          # harus: Found 30 skills

# pasang semua (30 skills + 8 commands + 2 personas)
npx skills add dimsdeall/my-skills

# atau satu skill saja
npx skills add dimsdeall/my-skills --skill brainstorming
```

Panduan per kategori (pilih 1 per 1 — Define/Plan/Build/Verify/Review/Ship/Explain/Personas) untuk Claude Code / OpenCode / Antigravity / CommandCode → [docs/installation.md](docs/installation.md)

## Cara Kerja — Lifecycle

Setiap fitur lewat kontrak yang sama. Satu spec = satu folder, tidak ada yang rilis tanpa lewat gate-nya.

```
/constraints (opsional, sekali — quality bar)
    │
IDEA ──→ SPEC ──→ PLAN ──→ BUILD ──→ VERIFY ──→ REVIEW ──→ SHIP ──→ OPERATE
 brainstorm  prd    impl-plan  code     tests    laporan   tag
 interview  WHAT/  + todos    RED→     + guard   5-axis   CHANGELOG
 idea-refine WHY    HOW+ORDER GREEN    hijau    → ADR    archive
```

| Tahap | Command | Yang dilakukan | Gate |
|-------|---------|----------------|------|
| **Constraints** | `/constraints` | Interview 4Q → tulis `docs/CONSTRAINTS.md` (Floor + Enforced with numbers + Exceptions), pasang `check:fast/task/full` | Sekali di awal repo |
| **Spec** | `/spec` | `brainstorming` hard-gate (Spike/Bounded/Architectural) → Socratic refine → `prd.md` (8 section: Goal, Persona, Stories, Requirements, AC…) | **STOP** — tunggu approval eksplisit Kak |
| **Plan** | `/plan` | Baca `prd.md` → `implementation-plan.md` (Mermaid 5-layer + ERD + API + frontend) → `todo.md` (vertical slices) | Approval plan |
| **Build** | `/build` | Loop TDD RED→GREEN→regression, 1 task = 1 commit conventional, tandai `[x]` di `todo.md` | Tests + build hijau |
| **Verify** | `/verify` | Full suite + debug + kondisional security/perf/web (web **opsional** — skip untuk CLI/API-only) | Harus hijau sebelum review |
| **Review** | `/review` | Persona `code-reviewer` — laporan 5-axis (Critical/Important/Suggestion + `file:line`) | Fix Critical sebelum ship |
| **Ship** | `/ship` | Fan-out `code-reviewer` + `security-auditor` → GO/NO-GO + rollback plan → `docs/specs/archive/` bila todo 100% | Archive hanya bila 100% ✔ |

Alur lengkap & gate → [docs/lifecycle.md](docs/lifecycle.md) · Quality bar → [docs/constraints.md](docs/constraints.md)

## Commands (8 = 6 CORE + 2 OPTIONAL)

Slash command adalah **WHEN** — kapan lifecycle dijalankan. Tiap command mengorkestrasi persona (WHO) dan skill (HOW).

| Command | Fase | Output |
|---------|------|--------|
| `/spec` | SPEC | `docs/specs/active/<id>/prd.md` |
| `/plan` | PLAN | `implementation-plan.md` + `todo.md` |
| `/build` | BUILD | code + tests (1 commit per task) |
| `/verify` | VERIFY | gate hijau |
| `/review` | REVIEW | laporan `code-reviewer` + ADR di `docs/adr/` |
| `/ship` | SHIP | tag · CHANGELOG · `docs/specs/archive/<id>/` |
| `/constraints` | *opsional* | `docs/CONSTRAINTS.md` |
| `/explain-code` | *opsional, read-only* | arsitektur / skema / fitur |

Command = WHEN — komposisi persona (WHO) + skill (HOW). Kontrak per command → [docs/commands.md](docs/commands.md)

## Persona (2 — opsional, WHO)

Persona adalah perspektif spesialis — `Skill = HOW` · `Persona = WHO` · `Command = WHEN`.

| Persona | Peran | Dipakai di |
|---------|-------|------------|
| `code-reviewer` | Senior Staff Engineer — review 5-axis (correctness/readability/architecture/security/perf) | `/review` · `/ship` fan-out |
| `security-auditor` | Security Engineer — OWASP & threat modeling, hanya isu yang exploitable | `/ship` fan-out (kondisional — hanya bila spec sentuh auth/input) |

Persona tidak memanggil persona lain — komposisi ada di command. Detail → [docs/personas.md](docs/personas.md)

## Skills (30)

Dikelompokkan per lifecycle. Semua ada di `skills/<nama>/SKILL.md`.

| Kelompok | Jumlah | Highlight |
|----------|--------|-----------|
| **Define** | 5 | `brainstorming` (hard-gate), `interview-me`, `idea-refine`, `spec-driven-development`, `constraint-driven-development` |
| **Plan** | 3 | `planning-and-task-breakdown`, `context-engineering`, `using-agent-skills` |
| **Build** | 5 | `incremental-implementation`, `test-driven-development`, `api-and-interface-design`, `frontend-ui-engineering`, `source-driven-development` |
| **Verify** | 6 | `debugging-and-error-recovery`, `browser-testing-with-devtools`, `webapp-testing` *(web opsional)*, `security-and-hardening`, `performance-optimization`, `doubt-driven-development` |
| **Review** | 4 | `code-review-and-quality`, `code-simplification`, `documentation-and-adrs`, `deprecation-and-migration` |
| **Ship & Operate** | 4 | `git-workflow-and-versioning`, `ci-cd-and-automation`, `shipping-and-launch`, `observability-and-instrumentation` |
| **Explain** *(read-only, opsional)* | 3 | `improve-codebase-architecture`, `database-schema-designer`, `write-feature-docs` |

Tabel lengkap + sumber & checklist bersama (`references/` ×7) → [docs/skills.md](docs/skills.md)

## Struktur Development

**Repo ini (`my-skills`)** — library skill-nya sendiri:

```
my-skills/
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
