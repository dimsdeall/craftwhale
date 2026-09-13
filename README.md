# craftwhale

> *Building big ships for the ocean, accompanied by a whale.*

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
┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐
│ SPEC │ ───▶ │ PLAN │ ───▶ │BUILD │ ───▶ │VERIFY│ ───▶ │REVIEW│ ───▶ │ SHIP │
│I/PRD │      │ HOW  │      │ Code │      │ Test │      │ Gate │      │  Go  │
└──────┘      └──────┘      └──────┘      └──────┘      └──────┘      └──────┘
 /spec         /plan         /build       /verify       /review        /ship  