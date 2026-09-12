# Personas — WHO (2, Optional)

> `agents/*.md` — specialist perspectives. Skill = HOW, Persona = WHO, Command = WHEN.

## The Three Layers

| Layer | Job | Example |
|-------|-----|---------|
| **Skill** | Workflow with steps & exit criteria | `code-review-and-quality` |
| **Persona** | Role + perspective + output format | `code-reviewer` → 5-axis report |
| **Command** | User-facing entry point that composes them | `/review`, `/ship` |

Personas do **not** invoke other personas — composition lives in slash commands or the user.

## The 2 Personas

| Persona | Role | When | Source |
|---------|------|------|--------|
| `code-reviewer` | Senior Staff Engineer — 5-axis review (correctness / readability / architecture / security / performance) with "would a staff engineer approve this?" standard | `/review` (single) & `/ship` fan-out | `addyosmani/agent-skills` |
| `security-auditor` | Security Engineer — vulnerability detection, threat modeling, OWASP assessment, focuses on exploitable issues | `/ship` fan-out, **conditional** — only if the spec touches auth / input / sessions / external integrations / deps | `addyosmani/agent-skills` |

Files: `agents/code-reviewer.md`, `agents/security-auditor.md` (Markdown consumed as system prompt).

## How They Compose with Commands

- **Direct persona** — "review this PR" → invoke `code-reviewer` directly (no command needed).
- **Single-persona command** — `/review` wraps `code-reviewer` + review skills.
- **Orchestrator fan-out** — `/ship` spawns `code-reviewer` + `security-auditor` in parallel, then the main agent merges their reports into a GO/NO-GO. This is the only endorsed orchestration pattern — see `references/orchestration-patterns.md` and `docs/commands.md`.

```
 /review (single)
   └─ code-reviewer → 5-axis report (Critical / Important / Suggestion + file:line)

 /ship (orchestrator)
   ├── (parallel) code-reviewer    → review report
   └── (parallel) security-auditor → audit report  (skipped if non-security spec)
                      ↓ merge (main agent)
               GO / NO-GO + rollback plan + archive gate
```

## Rules

1. One persona = one role + one output format.
2. Personas do not invoke other personas (also a Claude Code platform constraint — subagents cannot spawn subagents).
3. A persona may invoke skills (the HOW).
4. Every persona file ends with a Composition block stating where it fits.

See also: `docs/skills.md` (the HOW), `docs/commands.md` (the WHEN), `docs/lifecycle.md` (end-to-end flow).
