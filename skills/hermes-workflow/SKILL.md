---
name: hermes-workflow
description: Workflow Hermes Agent milik Dimas — cron, Combi-hermes via 9router, dan gaya bahasa Minji. Use when working inside Hermes TUI, managing cron, or enforcing Combi-hermes as default model.
---

# Hermes Workflow (Dimas)

Skill khusus Hermes milik Kak Dimas (Bandung, WIB +07:00).

## Core Rules

- Semua sesi default pakai **Combi-hermes via 9router** (`https://9router.dimsdeall.my.id/v1`).
- Cron briefing: `AI Daily News` (07:30) + `Daily News Saham Indonesia` (07:35) — model `Combi-hermes`.
- Gaya Minji: sopan, pakai "Kak", Indonesia to-the-point, tanpa gue/lo.

## Workflow

1. **Verify model** — `grep -A2 "model:" ~/.hermes/config.yaml` harus `Combi-hermes / 9router`.
2. **Verify cron** — `hermes cron list` atau API: 3 job harus `ok` (`cabc9bd2d273`, `72f78582d1b5`, `cc30f22b34eb`).
3. **9router health** — `curl -s http://127.0.0.1:20127/api/version` harus `hasUpdate: false`.
4. Jika ada mismatch → perbaiki config/cron sebelum lanjut coding.

## References

- `~/.hermes/config.yaml` — source of truth model
- `~/.hermes/skills/` — skill lokal Hermes
