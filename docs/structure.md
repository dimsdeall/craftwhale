# Structure — Where Files Live

> All docs output lives under `docs/`. Per-spec folders keep work isolated.

## Consumer Project Layout (the project you apply my-skills to)

```
project-root/
├── docs/
│   ├── CONSTRAINTS.md                   # /constraints — canonical (once)
│   ├── specs/
│   │   ├── active/                      # in-progress specs
│   │   │   ├── 2026-09-13-user-auth/
│   │   │   │   ├── prd.md               # /spec  — WHAT & WHY (8 sections)
│   │   │   │   ├── implementation-plan.md # /plan Phase 1 — HOW
│   │   │   │   └── todo.md              # /plan Phase 2 — ORDER
│   │   │   ├── 2026-09-14-billing/
│   │   │   └── 2026-09-15-notifications/ # collides? /spec asks Merge / Split / Defer
│   │   └── archive/                     # done — moved by /ship only when todos 100%
│   │       └── 2026-09-10-legacy-auth/
│   ├── adr/                             # ADRs from /review (via code-reviewer persona)
│   │   └── ADR-0001-*.md
│   └── explain/                         # /explain-code — saved only on request
│       ├── architecture-2026-09-13.md
│       ├── schema-2026-09-13.md
│       └── features-2026-09-13.md
├── src/, tests/, package.json, etc.     # code — written by /build (1 task = 1 commit)
└── /tmp/architecture-review-*.html      # /explain-code (a) — temp, not in repo
```

## Rules Enforced in `commands/*.toml`

| Rule | Where | How |
|------|-------|-----|
| Everything in `docs/` | `docs/specs/active/<spec-id>/` | No docs in repo root or `tasks/` |
| New spec = new folder | `docs/specs/active/YYYY-MM-DD-<slug>/` | Each `/spec` creates a new `<spec-id>`; `/plan`+`/build` read from it |
| Collision → ask | `/spec` step 7 & `/plan` guard | Scan active prd/plan/todo overlap + unchecked todos → STOP → **(a) Merge** into active spec, **(b) Split** (new parallel folder), **(c) Defer** |
| Done → archive | `/ship` step 7 | `git mv docs/specs/active/<id> docs/specs/archive/<id>` only when every `- [ ]` → `- [x]` |

## This Repo's Own Layout (my-skills)

> `docs/` here holds **only** the 8 technical docs + index. Consumer-only folders (`specs/`, `adr/`, `explain/`, `CONSTRAINTS.md`) live in **consumer projects**, not in this repo.

```
my-skills/
├── agents/*.md                    # 2 personas: code-reviewer, security-auditor (WHO)
├── commands/*.toml                # 8 commands: 6 CORE + 2 OPTIONAL
├── skills/<name>/SKILL.md         # 30 skills (see docs/skills.md)
│   └── scripts/, references/      # per-skill (e.g. brainstorming)
├── references/                    # 7 shared checklists
│   ├── accessibility-checklist.md
│   ├── definition-of-done.md
│   ├── observability-checklist.md
│   ├── orchestration-patterns.md
│   ├── performance-checklist.md
│   ├── security-checklist.md
│   └── testing-patterns.md
├── docs/                          # you are here — 8 docs + index only
│   ├── README.md                  # index — links to all 8
│   ├── lifecycle.md               # Idea → Ship flow
│   ├── skills.md                  # all 30 skills
│   ├── personas.md                # 2 personas
│   ├── commands.md                # 6+2 commands
│   ├── structure.md               # ← this file
│   ├── constraints.md             # quality bar
│   ├── explaining.md              # /explain-code lenses
│   └── installation.md            # how to install & update
├── AGENTS.md                      # machine-readable inventory & intent map
├── plugin.json                    # registry metadata (name/version/owner)
├── README.md                      # English (default) — light entry point
└── README.id.md                   # Indonesian mirror
```

> `docs/specs/`, `docs/adr/`, `docs/explain/`, `docs/CONSTRAINTS.md` are **not** in this repo. They are created by `/spec` → `/ship` inside the project that *uses* my-skills (see Consumer layout above).

## Adding a New Skill

```bash
cp -r skills/spec-driven-development skills/my-new-skill
# edit skills/my-new-skill/SKILL.md — change frontmatter name & description (must == folder name)
git add skills/my-new-skill && git commit -m "feat: add my-new-skill" && git push
# verify
npx skills add dimsdeall/my-skills --skill my-new-skill --list
```
