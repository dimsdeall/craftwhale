# my-skills — Dimas Putra (dimsdeall)

Kumpulan **Agent Skills** milik Kak Dimas — workflow Hermes, 9Router, dan template umum. Terinspirasi oleh [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills), tapi ini versi milik sendiri.

Pasang via CLI `skills` (70+ agent: Claude Code, Codex, Cursor, OpenCode, dll):

```bash
# lihat dulu apa aja yang ada
npx skills add dimsdeall/my-skills --list

# pasang semua
npx skills add dimsdeall/my-skills

# pasang satu skill aja
npx skills add dimsdeall/my-skills --skill hello-world
npx skills add dimsdeall/my-skills --skill hermes-workflow
npx skills add dimsdeall/my-skills --skill 9router-ops
```

## Daftar Skill

| Skill | Deskripsi |
|-------|-----------|
| `hello-world` | Template minimal — buat tes instalasi & starter skill baru |
| `hermes-workflow` | Workflow Hermes Agent: cron + Combi-hermes via 9router + gaya Minji |
| `9router-ops` | Operasional 9Router gateway (PM2, build, update v0.5.69→v0.5.75) |

> Mau nambah skill baru? Duplikasi `skills/hello-world/` → ganti `name` & `description` di frontmatter `SKILL.md` → push.

## Struktur

```
my-skills/
├── skills/<nama-skill>/SKILL.md   # tiap skill = 1 folder + 1 SKILL.md (wajib)
├── references/                      # checklist/shared docs (opsional)
├── docs/                            # panduan tambahan
├── AGENTS.md                        # panduan untuk AI agent yang ngerjain repo ini
├── plugin.json                      # metadata marketplace
└── README.md
```

## Cara buat skill baru (30 detik)

```bash
cp -r skills/hello-world skills/nama-skill-baru
# edit skills/nama-skill-baru/SKILL.md -> ganti name & description di frontmatter
# edit isi workflow-nya, lalu:
git add skills/nama-skill-baru && git commit -m "feat: add nama-skill-baru" && git push
```

## Instal lokal (OpenCode)

```bash
mkdir -p .opencode/skills
cp -r /path/to/my-skills/skills/<nama> .opencode/skills/
# atau global
mkdir -p ~/.config/opencode/skills
cp -r /path/to/my-skills/skills/<nama> ~/.config/opencode/skills/
```

## Lisensi

MIT — bebas pakai & modifikasi.
