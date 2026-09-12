# Installation

> Repo is **private** — `gh auth login` as `dimsdeall` or be a collaborator.

## Quick Start (any agent, one command)

Uses the open `skills` CLI — works with 70+ agents (Claude Code, Cursor, Codex, Copilot, Cline, OpenCode, Hermes, and more).

```bash
# browse first
npx skills add dimsdeall/my-skills --list

# install all 30 skills + 8 commands + 2 personas
npx skills add dimsdeall/my-skills

# install one skill
npx skills add dimsdeall/my-skills --skill brainstorming
npx skills add dimsdeall/my-skills --skill spec-driven-development
```

## Updating

```bash
npx skills update          # update all installed skills
npx skills add dimsdeall/my-skills --list   # verify: Found 30 skills
```

## Local Copy (OpenCode / Hermes manual)

```bash
mkdir -p .opencode/skills
cp -r ~/projects/my-skills/skills/<name> .opencode/skills/
# personas (optional)
mkdir -p agents
cp ~/projects/my-skills/agents/*.md agents/
```

## Adding a Skill

```bash
cp -r skills/spec-driven-development skills/my-new-skill
# edit skills/my-new-skill/SKILL.md — change frontmatter name & description (must == folder name)
git add skills/my-new-skill && git commit -m "feat: add my-new-skill" && git push
```

## Verify

```bash
npx skills add dimsdeall/my-skills --list   # expect: Found 30 skills
ls agents/          # expect: code-reviewer.md  security-auditor.md
ls commands/*.toml  # expect: 8 files (6 CORE + 2 OPTIONAL)
```
