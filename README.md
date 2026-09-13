# craftwhale

> *Building big ships for the ocean, accompanied by a whale.*

> **English** | [Indonesia](README.id.md)

Production-grade agent skills — a full **Idea → Ship** lifecycle. **30 skills + 2 personas + 8 slash commands**, curated from open sources and wired to work together under one contract.

Works with 70+ agents (Claude Code, Cursor, Codex, Copilot, Cline, OpenCode, Hermes, etc.) via the open `skills` CLI.

## How It Works

Every feature follows the same contract. One spec = one folder, and nothing ships without passing its gates. `Command = WHEN` · `Skill = HOW` · `Persona = WHO`.

```
/constraints (optional, once — quality bar)
    │
┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐
│ SPEC │ ───▶ │ PLAN │ ───▶ │BUILD │ ───▶ │VERIFY│ ───▶ │REVIEW│ ───▶ │ SHIP │
│I/PRD │      │ HOW  │      │ Code │      │ Test │      │ Gate │      │  Go  │
└──────┘      └──────┘      └──────┘      └──────┘      └──────┘      └──────┘
 /spec         /plan         /build       /verify       /review        /ship  
```

| Phase | Command (WHEN) | Skills (HOW) | Output |
|-------|----------------|--------------|--------|
| **Constraints** *(once, optional)* | `/constraints` | `constraint-driven-development` — interview 4Q → Floor + Enforced + Exceptions | `docs/CONSTRAINTS.md` + `check:fast/task/full` |
| **Spec** | `/spec` | `brainstorming` (hard-gate) · `interview-me` · `idea-refine` · `spec-driven-development` | `docs/specs/active/<id>/prd.md` (8 sections: Goal, Personas, Stories, Requirements, AC) — **STOP for approval** |
| **Plan** | `/plan` | `planning-and-task-breakdown` · `context-engineering` · `using-agent-skills` | `implementation-plan.md` (Mermaid 5-layer + ERD + API + frontend) + `todo.md` (vertical slices) — approval |
| **Build** | `/build` | `incremental-implementation` · `test-driven-development` · `api-and-interface-design` · `frontend-ui-engineering` · `source-driven-development` | code + tests — 1 task = 1 commit `RED→GREEN→regression` |
| **Verify** | `/verify` | `debugging-and-error-recovery` · `browser-testing-with-devtools` · `webapp-testing` *(web optional)* · `security-and-hardening` · `performance-optimization` · `doubt-driven-development` | green tests + build — must pass before review |
| **Review** | `/review` | `code-review-and-quality` · `code-simplification` · `documentation-and-adrs` · `deprecation-and-migration` + `code-reviewer` persona (5-axis) | report `Critical/Important/Suggestion` + `file:line` + ADR — fix Critical before ship |
| **Ship** | `/ship` | `git-workflow-and-versioning` · `ci-cd-and-automation` · `shipping-and-launch` · `observability-and-instrumentation` + `code-reviewer` + `security-auditor` fan-out | tag · CHANGELOG · `docs/specs/archive/<id>/` (only when todos 100% ✔) — GO/NO-GO + rollback |
| **Explain** *(anytime, optional, read-only)* | `/explain-code` | `improve-codebase-architecture` · `database-schema-designer` · `write-feature-docs` | `docs/explain/` — architecture / schema / features |

> **30 skills** grouped above + `references/` ×7 shared checklists. Full tables, provenance & install per category (Define/Plan/Build/Verify/Review/Ship/Explain/Personas) → [docs/skills.md](docs/skills.md) · [docs/personas.md](docs/personas.md) · [docs/commands.md](docs/commands.md) · [docs/installation.md](docs/installation.md) · lifecycle gates → [docs/lifecycle.md](docs/lifecycle.md)

## Personas (2 — optional, WHO)

| Persona | Role | Used in |
|---------|------|---------|
| `code-reviewer` | Senior Staff Engineer — 5-axis review (correctness/readability/architecture/security/perf) | `/review` · `/ship` fan-out |
| `security-auditor` | Security Engineer — OWASP & threat modeling, exploitable issues only | `/ship` fan-out (conditional — only when spec touches auth/input) |

Personas don't call other personas — composition lives in the command. Detail → [docs/personas.md](docs/personas.md)

## Development Structure

**This repo (`craftwhale`)** — the skill library itself:

```
craftwhale/
├── agents/*.md          # 2 personas (WHO)
├── commands/*.toml      # 8 slash commands (WHEN)
├── skills/<name>/       # 30 skills (HOW)
├── references/          # 7 shared checklists
├── docs/                # technical docs (you are here)
└── README.md / README.id.md
```

**Consumer projects** (where you run `/spec` → `/ship`) — every artifact lives under `docs/`:

```
project-root/
└── docs/
    ├── CONSTRAINTS.md                 # from /constraints (once)
    ├── specs/
    │   ├── active/YYYY-MM-DD-<slug>/  # /spec creates one folder per spec
    │   │   ├── prd.md                 # WHAT & WHY
    │   │   ├── implementation-plan.md # HOW
    │   │   └── todo.md                # ORDER
    │   └── archive/<slug>/            # /ship moves here only when todos 100%
    ├── adr/                           # from /review
    └── explain/                       # from /explain-code (only on request)
```

Rules: new spec = new folder in `active/`; collision (overlap files/modules) → ask **Merge / Split / Defer**; archive only via `/ship` when every `- [ ]` → `- [x]`. Full layout & rules → [docs/structure.md](docs/structure.md)

## Docs

| Page | What you'll find |
|------|------------------|
| [docs/lifecycle.md](docs/lifecycle.md) | End-to-end Idea → Ship flow & gates |
| [docs/commands.md](docs/commands.md) | 8 slash commands — inputs, outputs, gates |
| [docs/personas.md](docs/personas.md) | 2 personas — roles & composition |
| [docs/skills.md](docs/skills.md) | All 30 skills — by group + provenance |
| [docs/structure.md](docs/structure.md) | File layout for this repo & for consumer projects |
| [docs/constraints.md](docs/constraints.md) | Quality bar (`docs/CONSTRAINTS.md`) |
| [docs/explaining.md](docs/explaining.md) | `/explain-code` — 3 read-only lenses |
| [docs/installation.md](docs/installation.md) | Install, update, local copy |

Browse the index → [docs/README.md](docs/README.md)

## License

MIT — free to use and modify.
