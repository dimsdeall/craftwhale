# craftwhale

> **English** | [Indonesia](README.id.md)

Production-grade agent skills — a full **Idea → Ship** lifecycle. **30 skills + 2 personas + 8 slash commands**, curated from open sources and wired to work together under one contract.

Works with 70+ agents (Claude Code, Cursor, Codex, Copilot, Cline, OpenCode, Hermes, etc.) via the open `skills` CLI.

## Install

```bash
# browse first
npx skills add dimsdeall/craftwhale --list          # expect: Found 30 skills

# install everything (30 skills + 8 commands + 2 personas)
npx skills add dimsdeall/craftwhale

# or one skill
npx skills add dimsdeall/craftwhale --skill brainstorming
```

Per-category manual (pick 1 by 1 — Define/Plan/Build/Verify/Review/Ship/Explain/Personas) for Claude Code / OpenCode / Antigravity / CommandCode → [docs/installation.md](docs/installation.md)

## How It Works — Lifecycle

Every feature follows the same contract. One spec = one folder, and nothing ships without passing its gates.

```
/constraints (optional, once — quality bar)
    │
IDEA ──→ SPEC ──→ PLAN ──→ BUILD ──→ VERIFY ──→ REVIEW ──→ SHIP ──→ OPERATE
 brainstorm  prd    impl-plan  code     tests    report    tag
 interview  WHAT/  + todos    RED→     + guard   5-axis   CHANGELOG
 idea-refine WHY    HOW+ORDER GREEN    green    → ADR    archive
```

| Step | You run | What it does | Gate |
|------|---------|--------------|------|
| **Constraints** | `/constraints` | Interviews (4Q) → writes `docs/CONSTRAINTS.md` (Floor + Enforced with numbers + Exceptions), wires `check:fast/task/full` | Once at repo start |
| **Spec** | `/spec` | `brainstorming` hard-gate (Spike/Bounded/Architectural) → Socratic refine → `prd.md` (8 sections: Goal, Personas, Stories, Requirements, AC…) | **STOP** — waits for your explicit approval |
| **Plan** | `/plan` | Reads `prd.md` → `implementation-plan.md` (Mermaid 5-layer + ERD + API + frontend) → `todo.md` (vertical slices) | Approval on plan |
| **Build** | `/build` | TDD loop RED→GREEN→regression, 1 task = 1 conventional commit, marks `[x]` in `todo.md` | Tests + build green |
| **Verify** | `/verify` | Full suite + debug + conditional security/perf/web (web is **optional** — skipped for CLI/API-only) | Must be green before review |
| **Review** | `/review` | `code-reviewer` persona — 5-axis report (Critical/Important/Suggestion + `file:line`) | Fix Critical before ship |
| **Ship** | `/ship` | Fan-out `code-reviewer` + `security-auditor` → GO/NO-GO + rollback plan → `docs/specs/archive/` when todos 100% | Archive only on 100% ✔ |

Full flow & gates → [docs/lifecycle.md](docs/lifecycle.md) · Quality bar → [docs/constraints.md](docs/constraints.md)

## Commands (8 = 6 CORE + 2 OPTIONAL)

Slash commands that drive the lifecycle — each one is the **WHEN**.

| Command | Phase | Output |
|---------|-------|--------|
| `/spec` | SPEC | `docs/specs/active/<id>/prd.md` |
| `/plan` | PLAN | `implementation-plan.md` + `todo.md` |
| `/build` | BUILD | code + tests (1 commit per task) |
| `/verify` | VERIFY | green gates |
| `/review` | REVIEW | `code-reviewer` report + ADR in `docs/adr/` |
| `/ship` | SHIP | tag · CHANGELOG · `docs/specs/archive/<id>/` |
| `/constraints` | *optional* | `docs/CONSTRAINTS.md` |
| `/explain-code` | *optional, read-only* | architecture / schema / features |

Commands are `WHEN` — they compose personas (WHO) and skills (HOW). Full contract per command → [docs/commands.md](docs/commands.md)

## Personas (2 — optional, WHO)

Personas are specialist perspectives — `Skill = HOW` · `Persona = WHO` · `Command = WHEN`.

| Persona | Role | Used in |
|---------|------|---------|
| `code-reviewer` | Senior Staff Engineer — 5-axis review (correctness/readability/architecture/security/perf) | `/review` · `/ship` fan-out |
| `security-auditor` | Security Engineer — OWASP & threat modeling, exploitable issues only | `/ship` fan-out (conditional — only when spec touches auth/input) |

Personas don't call other personas — composition lives in the command. Detail → [docs/personas.md](docs/personas.md)

## Skills (30)

Grouped by lifecycle. All live in `skills/<name>/SKILL.md`.

| Group | Count | Highlights |
|-------|-------|------------|
| **Define** | 5 | `brainstorming` (hard-gate), `interview-me`, `idea-refine`, `spec-driven-development`, `constraint-driven-development` |
| **Plan** | 3 | `planning-and-task-breakdown`, `context-engineering`, `using-agent-skills` |
| **Build** | 5 | `incremental-implementation`, `test-driven-development`, `api-and-interface-design`, `frontend-ui-engineering`, `source-driven-development` |
| **Verify** | 6 | `debugging-and-error-recovery`, `browser-testing-with-devtools`, `webapp-testing` *(web optional)*, `security-and-hardening`, `performance-optimization`, `doubt-driven-development` |
| **Review** | 4 | `code-review-and-quality`, `code-simplification`, `documentation-and-adrs`, `deprecation-and-migration` |
| **Ship & Operate** | 4 | `git-workflow-and-versioning`, `ci-cd-and-automation`, `shipping-and-launch`, `observability-and-instrumentation` |
| **Explain** *(read-only, optional)* | 3 | `improve-codebase-architecture`, `database-schema-designer`, `write-feature-docs` |

Full table + sources & shared checklists (`references/` ×7) → [docs/skills.md](docs/skills.md)

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
