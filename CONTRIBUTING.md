# Contributing to craftwhale

Thanks for considering a contribution! This repo is a curated skill library — **30 skills + 2 personas + 8 slash commands** — with a strict layout so every agent (Claude Code, OpenCode, Antigravity, CommandCode, Hermes, …) can discover them.

> **Language:** This file is in English (default). Indonesian version? PR welcome as `CONTRIBUTING.id.md`.

## Ground Rules

- **One PR per change.** Small, focused PRs are reviewed faster.
- **Conventional commits:** `feat:`, `fix:`, `docs:`, `chore:`, `refactor:`. Example: `feat: add my-new-skill`.
- **No force-push to `main`.** Open a branch → PR → review → merge.
- **License:** By contributing you agree your work is under **MIT** (see `LICENSE`).

## What Can You Contribute?

| Area | Where | What |
|------|-------|------|
| **Skill** | `skills/<name>/SKILL.md` | A reusable workflow (Define/Plan/Build/Verify/Review/Ship/Explain) |
| **Persona** | `agents/<name>.md` | A specialist perspective — `Skill = HOW · Persona = WHO · Command = WHEN` |
| **Command** | `commands/<name>.toml` | A slash entry point (`/spec`, `/plan`, …) that composes skills + personas |
| **Docs** | `docs/*.md` | Lifecycle, skills, personas, commands, structure, installation |
| **Checklist** | `references/*.md` | Shared checklist used by multiple skills |

## Adding a New Skill

```bash
# 1. Clone & branch
git clone https://github.com/dimsdeall/craftwhale.git
cd craftwhale
git checkout -b feat/add-my-skill

# 2. Copy the closest skill as template
cp -r skills/spec-driven-development skills/my-new-skill

# 3. Edit frontmatter — name MUST == folder name (lowercase, hyphen)
#    skills/my-new-skill/SKILL.md
#    ---
#    name: my-new-skill
#    description: One-line description. Use when ...
#    ---

# 4. Write the workflow: Overview → When to Use → Process → Verification

# 5. Register in docs
#    - Add row to docs/skills.md (right group table)
#    - If it belongs to a category, add to docs/installation.md category table

# 6. Verify locally
npx skills add dimsdeall/craftwhale --list   # expect: Found 31 skills (was 30)

# 7. Commit & push
git add skills/my-new-skill docs/skills.md docs/installation.md
git commit -m "feat: add my-new-skill"
git push -u origin feat/add-my-skill
# then open PR on GitHub
```

### Skill Anatomy (keep it minimal)

Every `SKILL.md` follows:

```
Frontmatter (name + description)
Overview        → what it does
When to Use     → triggering conditions
Process         → step-by-step workflow
Verification    → evidence required (tests, build, screenshot, …)
```

See `docs/skill-anatomy.md` in `addyosmani/agent-skills` for the full spec.

## Adding a Persona

```bash
cp agents/code-reviewer.md agents/my-reviewer.md
# edit frontmatter + role + scope + output format
# add to docs/personas.md table + docs/skills.md if needed
```

Rules: one persona = one role + one output format. Personas **do not** invoke other personas — composition lives in commands.

## Adding a Command

Commands are `commands/<name>.toml`:

```toml
description = "MY-CMD — one-line"
prompt = """
Invoke <skill/persona> as orchestrator ...
"""
```

Register in `docs/commands.md` and update `README.md` / `README.id.md` tables if needed.

## Docs-Only Changes

- Keep `README.md` light — deep detail belongs in `docs/`.
- `README.md` = English (default), `README.id.md` = Indonesian mirror — update both.
- `docs/README.md` is the navigational index — add new pages there.

## Branch & PR Flow

```
main  ← PR ←  feat/add-xyz  /  fix/abc  /  docs/update-xyz
```

1. Branch from `main`.
2. Keep PR description short: **what / why / how verified**.
3. Ensure `npx skills add dimsdeall/craftwhale --list` still passes.
4. One approval → squash-merge.

## Reporting Issues

Open an issue with:

- **What** you expected vs what happened
- **Steps** to reproduce
- **Agent** + version (Claude Code / OpenCode / Antigravity / CommandCode)
- **Skill/command** involved

## Questions?

Open a GitHub Discussion or issue — or ping **@dimsdeall**.

Happy crafting 🐋 — *craft deep, ship big!*
