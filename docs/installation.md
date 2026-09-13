# Installation

> Works with 70+ agents via the open `skills` CLI: `npx skills add dimsdeall/craftwhale --list` → `npx skills add dimsdeall/craftwhale`.
> This page is the **per-category manual** — pick only what you need, for the agent you use.

## 1. Pick by Category — What Do You Want to Install?

Don't install everything if you don't need it. Pick categories one by one.

| Category | When you need it | Skills in it | Also needed |
|----------|------------------|--------------|-------------|
| **Define** | Clarify what to build — ideas, interviews, PRD | `brainstorming` · `interview-me` · `idea-refine` · `spec-driven-development` · `constraint-driven-development` | — |
| **Plan** | Break a spec into ordered tasks | `planning-and-task-breakdown` · `context-engineering` · `using-agent-skills` | Requires a `prd.md` from Define |
| **Build** | Write code incrementally | `incremental-implementation` · `test-driven-development` · `api-and-interface-design` · `frontend-ui-engineering` · `source-driven-development` | Requires `todo.md` from Plan |
| **Verify** | Prove it works — debug, security, perf | `debugging-and-error-recovery` · `security-and-hardening` · `performance-optimization` · `doubt-driven-development` · `browser-testing-with-devtools` · `webapp-testing` *(web only, optional)* | Run after Build |
| **Review** | Quality gate before merge | `code-review-and-quality` · `code-simplification` · `documentation-and-adrs` · `deprecation-and-migration` | Run after Verify is green |
| **Ship & Operate** | Release & observe | `git-workflow-and-versioning` · `ci-cd-and-automation` · `shipping-and-launch` · `observability-and-instrumentation` | Run after Review |
| **Explain** *(optional, read-only)* | Understand existing code — no code changed | `improve-codebase-architecture` · `database-schema-designer` · `write-feature-docs` | Anytime, standalone |
| **Personas** *(optional, WHO)* | Specialist perspective for review/ship | `code-reviewer` · `security-auditor` | Used by `/review` & `/ship` |
| **Shared references** | Checklists used by multiple skills | `references/` (7 files: accessibility, definition-of-done, observability, orchestration, performance, security, testing) | Copy if a skill references them |
| **Commands** *(WHEN)* | Slash entry points for the lifecycle | `commands/*.toml` → 8 commands: `/spec` `/plan` `/build` `/verify` `/review` `/ship` + `/constraints` `/explain-code` | One per lifecycle step |

> Tip: Start with **Define** alone. Add **Plan → Build** when the PRD is approved. Add **Verify → Review → Ship** when code exists.

## 2. Get the Repo (once)

```bash
# via gh
gh repo clone dimsdeall/craftwhale /tmp/craftwhale

# or https
git clone https://github.com/dimsdeall/craftwhale.git /tmp/craftwhale
```

Or use the open `skills` CLI per-skill (copies only `skills/<name>/`, not `references/`):

```bash
npx skills add dimsdeall/craftwhale --skill brainstorming   # one skill
npx skills add dimsdeall/craftwhale --list                  # browse
```

> Per-skill `npx` copies only `skills/<name>/` — shared `references/` is not included. If a skill needs a checklist, copy `references/` manually (see each agent below).

## 3. Install by Agent — Copy Only the Categories You Picked

Each agent discovers skills from different paths. Project-local = this repo only. Global = every project on this machine.

| Agent | Skills (project) | Skills (global) | Commands | Personas | Global config |
|-------|------------------|-----------------|----------|----------|---------------|
| **Claude Code** | `.claude/skills/<name>/` | `~/.claude/skills/<name>/` | `.claude/commands/*.md` | `.claude/agents/*.md` | Marketplace: `/plugin marketplace add dimsdeall/craftwhale` |
| **OpenCode** | `.opencode/skills/<name>/` | `~/.config/opencode/skills/<name>/` | `.opencode/commands/*.md` | `agents/*.md` (or `.opencode/prompts/agents/`) | Also reads `.claude/skills/` & `.agents/skills/` |
| **Antigravity (agy)** | Native plugin — `agy plugin install <path-or-url>` (skills auto-discovered) | `~/.gemini/config/plugins/craftwhale/` | Legacy `commands/*.toml` wrappers not exposed in agy 1.1.x — invoke skill directly | `agents/*.md` inside plugin | `agy plugin list` / `agy plugin validate` |
| **CommandCode (cmd)** | `.commandcode/skills/<name>/` | `~/.commandcode/skills/<name>/` | Slash menu auto-discovers skills — `[skill]` tag | `agents/*.md` | Also reads `.agents/skills/<name>/` |

### Claude Code

```bash
# from your project root — assumes /tmp/craftwhale exists
# Example: install only Define (5) + Plan (3)
mkdir -p .claude/skills
for s in brainstorming interview-me idea-refine spec-driven-development constraint-driven-development \
         planning-and-task-breakdown context-engineering using-agent-skills; do
  cp -r /tmp/craftwhale/skills/$s .claude/skills/
done

# Add a category later — e.g. Build
for s in incremental-implementation test-driven-development api-and-interface-design \
         frontend-ui-engineering source-driven-development; do
  cp -r /tmp/craftwhale/skills/$s .claude/skills/
done

# Verify — only if needed (checklists referenced by skills)
mkdir -p .claude/skills/references 2>/dev/null; cp -r /tmp/craftwhale/references .claude/ 2>/dev/null || cp -r /tmp/craftwhale/references .claude/skills/references

# Commands (optional — lifecycle entry points)
mkdir -p .claude/commands
cp /tmp/craftwhale/commands/*.toml .claude/commands/ 2>/dev/null || cp /tmp/craftwhale/commands/*.md .claude/commands/ 2>/dev/null || true
# If using the legacy command TOMLs, convert per your Claude setup (some versions expect .md)

# Personas (optional — WHO for /review & /ship)
mkdir -p .claude/agents
cp /tmp/craftwhale/agents/*.md .claude/agents/

# Global (all projects)
mkdir -p ~/.claude/skills && cp -r /tmp/craftwhale/skills/<name> ~/.claude/skills/
```

Alternative marketplace (if published):

```bash
/plugin marketplace add dimsdeall/craftwhale
/plugin install craftwhale@craftwhale
```

### OpenCode

```bash
# Project-local
mkdir -p .opencode/skills
# Example: Define only
for s in brainstorming interview-me idea-refine spec-driven-development constraint-driven-development; do
  cp -r /tmp/craftwhale/skills/$s .opencode/skills/
done
# Add more categories the same way — e.g. Verify (web optional: skip webapp-testing if not a web project)
for s in debugging-and-error-recovery security-and-hardening performance-optimization doubt-driven-development browser-testing-with-devtools; do
  cp -r /tmp/craftwhale/skills/$s .opencode/skills/
done
# Optional web verification (only for web projects)
cp -r /tmp/craftwhale/skills/webapp-testing .opencode/skills/

# Shared references (copy once if any installed skill needs them)
cp -r /tmp/craftwhale/references .opencode/references 2>/dev/null; cp -r /tmp/craftwhale/references ./references 2>/dev/null || true

# Commands (optional)
mkdir -p .opencode/commands
cp /tmp/craftwhale/commands/*.toml .opencode/commands/ 2>/dev/null; cp /tmp/craftwhale/commands/*.md .opencode/commands/ 2>/dev/null || true
# Add to .opencode/opencode.json if you use command.paths:
# "command": { "paths": { "commands": [".opencode/commands"], "template": ".opencode/commands" } }

# Personas
mkdir -p agents && cp /tmp/craftwhale/agents/*.md agents/

# Global (all projects)
mkdir -p ~/.config/opencode/skills
cp -r /tmp/craftwhale/skills/<name> ~/.config/opencode/skills/

# Cross-compatible fallback (OpenCode also reads these)
mkdir -p .agents/skills && cp -r /tmp/craftwhale/skills/<name> .agents/skills/
```

Verify config schema after editing `.opencode/opencode.json[c]`:

```bash
timeout 40 opencode run --model litellm/openagentic/claude-sonnet-4.6 "Reply with just: OK config loaded"
# expect no "Configuration is invalid" error
```

### Antigravity (agy)

Antigravity installs the whole repo as a native plugin — then invoke skills per category (one by one).

```bash
# Recommended — from remote
agy plugin install https://github.com/dimsdeall/craftwhale.git

# Or from local clone
agy plugin install /tmp/craftwhale

# Verify
agy plugin list
agy plugin validate /tmp/craftwhale

# Invoke per category — one at a time, as needed
# Define:
/agent-skills:spec-driven-development
# Plan:
/agent-skills:planning-and-task-breakdown
# Build:
/agent-skills:incremental-implementation
/agent-skills:test-driven-development
# Verify (pick what applies):
/agent-skills:debugging-and-error-recovery
/agent-skills:security-and-hardening
# Review:
/agent-skills:code-review-and-quality
# Ship:
/agent-skills:shipping-and-launch
# Explain (read-only):
# /agent-skills:improve-codebase-architecture  (via /explain-code)
```

> Note: In agy 1.1.x, legacy wrappers `commands/*.toml` (`/spec`, `/build`, etc.) are reported as "converted" but don't appear in the slash menu. Invoke the skill directly as shown above (tracked in `addyosmani/agent-skills#445`).

Global plugin path: `~/.gemini/config/plugins/craftwhale/` (not the legacy `~/.gemini/antigravity-cli/plugins/`).

### CommandCode (cmd)

`cmd skills add` already asks **per skill** in an interactive terminal (multi-select). Use it category by category.

```bash
# Interactive — shows all 30 skills, pick one category at a time
cmd skills add dimsdeall/craftwhale              # project scope → .commandcode/skills/
# In the TUI: check only Define (5), confirm → repeat for the next category

# Non-interactive — one skill at a time
cmd skills add dimsdeall/craftwhale -s brainstorming
cmd skills add dimsdeall/craftwhale -s interview-me
cmd skills add dimsdeall/craftwhale -s spec-driven-development

# Global (all projects)
cmd skills add dimsdeall/craftwhale --global
cmd skills add dimsdeall/craftwhale -s brainstorming --global

# Manual copy (alternative)
mkdir -p .commandcode/skills
for s in brainstorming interview-me idea-refine spec-driven-development constraint-driven-development; do
  cp -r /tmp/craftwhale/skills/$s .commandcode/skills/
done
# Also reads .agents/skills/
mkdir -p .agents/skills && cp -r /tmp/craftwhale/skills/<name> .agents/skills/
```

Manage:

```bash
cmd skills list                                    # list installed
cmd skills remove brainstorming                    # remove project-scoped
cmd skills remove brainstorming --global           # remove global
cmd skills add dimsdeall/craftwhale --force         # update / overwrite
```

Skills appear in the TUI slash menu as `/spec-driven-development   [skill]`.

## 4. Verify

```bash
# Skills CLI (any agent)
npx skills add dimsdeall/craftwhale --list   # expect: Found 30 skills

# Per-agent checks
ls .claude/skills/          2>/dev/null | wc -l       # Claude
ls .opencode/skills/        2>/dev/null | wc -l       # OpenCode
ls .commandcode/skills/     2>/dev/null | wc -l       # CommandCode
agy plugin list             2>/dev/null               # Antigravity
ls agents/*.md              2>/dev/null               # personas
ls commands/*.toml          2>/dev/null | wc -l       # commands (8)
```

## 5. Updating — Also Per Category

```bash
# Skills CLI — update all or one
npx skills update
npx skills add dimsdeall/craftwhale --skill <name> --force

# Manual — re-copy only the categories you use
cp -r /tmp/craftwhale/skills/<name> .claude/skills/        # or .opencode/skills/ / .commandcode/skills/
agy plugin install /tmp/craftwhale --force 2>/dev/null || agy plugin install https://github.com/dimsdeall/craftwhale.git
cmd skills add dimsdeall/craftwhale -s <name> --force
```

## 6. Adding a New Skill to This Repo

```bash
cp -r skills/spec-driven-development skills/my-new-skill
# edit skills/my-new-skill/SKILL.md — change frontmatter name & description (must == folder name)
git add skills/my-new-skill && git commit -m "feat: add my-new-skill" && git push
```

Category assignment: add the new skill to the right table in `docs/skills.md` and this file so users can pick it per category.
