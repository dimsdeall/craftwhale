# craftwhale

> *Membangun kapal besar untuk lautan, didampingi paus.*

> [English](README.md) | **Indonesia**

Kumpulan agent skills production-grade — lifecycle lengkap **Idea → Ship**. **30 skills + 2 persona + 8 slash command**, dikurasi dari sumber terbuka dan dirangkai dalam satu kontrak.

Kompatibel dengan 70+ agent (Claude Code, Cursor, Codex, Copilot, Cline, OpenCode, Hermes, dll.) via CLI open `skills`.

## Instalasi

```bash
# lihat dulu
npx skills add dimsdeall/craftwhale --list          # harus: Found 30 skills

# pasang semua (30 skills + 8 commands + 2 personas)
npx skills add dimsdeall/craftwhale

# atau satu skill saja
npx skills add dimsdeall/craftwhale --skill brainstorming
```

Panduan per kategori (pilih 1 per 1 — Define/Plan/Build/Verify/Review/Ship/Explain/Personas) untuk Claude Code / OpenCode / Antigravity / CommandCode → [docs/installation.md](docs/installation.md)

## Cara Kerja — Lifecycle

Setiap fitur lewat kontrak yang sama. Satu spec = satu folder, tidak ada yang rilis tanpa lewat gate-nya.

```
/constraints (opsional, sekali — quality bar)
    │
┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐      ┌──────┐
│ SPEC │ ───▶ │ PLAN │ ───▶ │BUILD │ ───▶ │VERIFY│ ───▶ │REVIEW│ ───▶ │ SHIP │
│I/PRD │      │ HOW  │      │ Code │      │ Test │      │ Gate │      │  Go  │
└──────┘      └──────┘      └──────┘      └──────┘      └──────┘      └──────┘
 /spec         /plan         /build       /verify       /review        /ship  