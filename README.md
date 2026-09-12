# my-skills — Dimas Putra (dimsdeall)

Kumpulan **Agent Skills** lifecycle lengkap Idea → Ship. Dikurasi dari [addyosmani/agent-skills](https://github.com/addyosmani/agent-skills) (25 skills) + [obra/superpowers — brainstorming](https://agenticskills.io/skills/brainstorming) + 3 explain skills (architecture/schema/feature) + 1 web verification. Total **30 skills**.

Pasang via CLI `skills` (70+ agent: Claude Code, Codex, Cursor, OpenCode, Hermes, dll):

```bash
# lihat dulu apa aja yang ada
npx skills add dimsdeall/my-skills --list

# pasang semua
npx skills add dimsdeall/my-skills

# pasang satu skill aja
npx skills add dimsdeall/my-skills --skill brainstorming
npx skills add dimsdeall/my-skills --skill spec-driven-development
```

> Repo ini **private** — instal butuh `gh auth login` sebagai `dimsdeall` atau jadi collaborator.

## Lifecycle — Idea → Ship

```
/constraints (opsional, sekali — quality bar)
    │
IDEA ──→ SPEC ──→ PLAN ──→ BUILD ──→ VERIFY ──→ REVIEW ──→ SHIP ──→ OPERATE
  │        │       │        │         │          │        │        │
  brainstorm  spec   planning incremental debug  code   shipping observability
  interview  (PRD)  (HOW+    + TDD   +recovery review + CI/CD  + monitor
  idea-refine WHAT/  ORDER)  +context                 + deprecation
              WHY   impl-plan +source-driven
                    + tasks
```

**Kontrak per fase (yang Kak setujui):**
- `/constraints` — sekali di awal (opsional)
- `/spec`  → `prd.md` (WHAT & WHY) — approval
- `/plan`  → `implementation-plan.md` (HOW) + `tasks/plan.md` (ORDER) — approval
- `/build` → code (RED→GREEN per task)

## Daftar Skill (30)

### Define — Mau bikin apa? (5)
| Skill | Deskripsi |
|-------|-----------|
| `brainstorming` | **Gerbang pertama** — klasifikasi Spike/Bounded/Architectural, Socratic refinement, hard-gate approval sebelum coding (obra/superpowers, S-rank) |
| `interview-me` | Interogasi requirement satu pertanyaan per pesan |
| `idea-refine` | Varian ide & pematangan konsep |
| `spec-driven-development` | Tulis spec/PRD sebelum coding — source of truth |
| `constraint-driven-development` | Tetapkan quality bar sekali, enforce di mana-mana |

### Plan — Gimana ngerjainnya? (3)
| Skill | Deskripsi |
|-------|-----------|
| `planning-and-task-breakdown` | Pecah spec jadi task atomik + acceptance criteria |
| `context-engineering` | Siapkan konteks repo: struktur, pola existing |
| `using-agent-skills` | Meta-skill — routing intent → skill yang tepat |

### Build — Ngerjainnya (5)
| Skill | Deskripsi |
|-------|-----------|
| `incremental-implementation` | Satu slice satu commit, jangan big bang |
| `test-driven-development` | RED-GREEN-REFACTOR, coverage 80%+ |
| `api-and-interface-design` | Desain API & interface |
| `frontend-ui-engineering` | Engineering UI |
| `source-driven-development` | Bukti dari docs/code sebelum nulis |

### Verify — Yakin bener? (6, web opsional)
| Skill | Deskripsi |
|-------|-----------|
| `debugging-and-error-recovery` | Reproduksi → lokalisasi → fix → guard |
| `browser-testing-with-devtools` | Testing via browser automation |
| `security-and-hardening` | Hardening & vulnerability check |
| `performance-optimization` | Optimasi performa |
| `doubt-driven-development` | Stakes tinggi / code asing — verifikasi ekstra |
| `webapp-testing` | **Opsional — hanya web** — Playwright + `with_server.py`, screenshot & console log (Anthropic) |

### Review — Layak merge? (4)
| Skill | Deskripsi |
|-------|-----------|
| `code-review-and-quality` | Review 5 axis: correctness, design, readability, test, security |
| `code-simplification` | Clarity over cleverness |
| `documentation-and-adrs` | ADR & dokumentasi keputusan arsitektur |
| `deprecation-and-migration` | Deprecation & migrasi yang aman |

### Ship & Operate (4)
| Skill | Deskripsi |
|-------|-----------|
| `git-workflow-and-versioning` | Branching, conventional commit, PR |
| `ci-cd-and-automation` | CI/CD pipeline |
| `shipping-and-launch` | Checklist rilis & go-live |
| `observability-and-instrumentation` | Log, metrik, alert, monitoring |

### Explain — Jelaskan yang sudah ada (3, opsional — read-only)
| Skill | Deskripsi | Sumber |
|-------|-----------|--------|
| `improve-codebase-architecture` | Scan arsitektur, deep-module opportunities, HTML report + Mermaid (915K) | `mattpocock/skills` |
| `database-schema-designer` | Desain & jelaskan DB/data-model schema, ERD, checklist | `softaworks/agent-toolkit` |
| `write-feature-docs` | Dokumentasi fitur dari codebase yang sudah ada | `warpdotdev/common-skills` |

## Struktur

Semua output ada di `docs/` — rapi, per-spec satu folder:

```
project-root/
├── docs/
│   ├── CONSTRAINTS.md                 ← /constraints (kanonikal, sekali)
│   ├── specs/
│   │   ├── active/                    ← sedang dikerjakan
│   │   │   ├── 2026-09-13-user-auth/  ← /spec baru = folder baru (YYYY-MM-DD-<slug>)
│   │   │   │   ├── prd.md             ← /spec — WHAT & WHY (8 section)
│   │   │   │   ├── implementation-plan.md ← /plan Phase 1 — HOW (5-layer Mermaid + ERD + API)
│   │   │   │   └── todo.md            ← /plan Phase 2 — ORDER (vertical slices, checklist)
│   │   │   ├── 2026-09-14-billing/    ← spec kedua — paralel bila tidak bersinggungan
│   │   │   │   ├── prd.md
│   │   │   │   ├── implementation-plan.md
│   │   │   │   └── todo.md
│   │   │   └── 2026-09-15-notifications/ ← bersinggungan? /spec tanya Gabung/Pisah/Tunda dulu
│   │   │       ├── prd.md
│   │   │       ├── implementation-plan.md
│   │   │       └── todo.md
│   │   └── archive/                   ← selesai — dipindah otomatis oleh /ship bila todo 100%
│   │       ├── 2026-09-10-legacy-auth/
│   │       │   ├── prd.md
│   │       │   ├── implementation-plan.md
│   │       │   └── todo.md            ← semua [x] — archive gate lolos
│   │       └── 2026-09-11-checkout/
│   ├── adr/                           ← ADR dari /review (bila ada keputusan arsitektur)
│   │   └── ADR-0001-*.md
│   └── explain/                       ← /explain-code — bila user minta save (read-only)
│       ├── architecture-2026-09-13.md
│       ├── schema-2026-09-13.md
│       └── features-2026-09-13.md
├── src/, tests/, package.json, etc.   ← kode — ditulis oleh /build (1 task = 1 commit)
└── $TMPDIR/architecture-review-*.html  ← /explain-code (a) — HTML report di temp OS, tidak di repo
```

**Aturan yang Kak minta (sudah di-enforce di commands/*.toml):**

| Aturan | Di mana | Cara kerja |
|--------|---------|------------|
| Semua di `docs/` | `docs/specs/active/<spec-id>/` | Tidak ada file docs di root repo atau `tasks/` — semua terkonsolidasi |
| Spec baru = folder baru | `docs/specs/active/YYYY-MM-DD-<slug>/` | Tiap `/spec` buat `<spec-id>` baru; pengerjaan `/plan` + `/build` baca dari folder spec tersebut |
| Bersinggungan → tanya | `/spec` step 7 & `/plan` collision guard | Scan `prd.md`/`implementation-plan.md`/`todo.md` aktif (file/module/capability/keyword overlap) + cek unchecked todos → STOP → tanya **(a) Gabung** (merge PRD ke spec aktif), **(b) Pisah** (folder baru paralel), **(c) Tunda** |
| Selesai → archive | `/ship` step 7 — archive gate | `git mv docs/specs/active/<id> docs/specs/archive/<id>` **hanya bila semua `- [ ]` sudah jadi `- [x]` di `todo.md`**; bila masih ada unchecked → tetap di `active`, tidak di-archive. Tidak pernah archive dari `/build`/`/verify` |

Dipakai oleh `my-skills` sendiri (`~/projects/my-skills`) juga sama:
```
my-skills/
├── commands/*.toml                  # 8 slash commands: 6 CORE (SPEC→SHIP) + 2 OPSIONAL (web verify opsional di /verify)
├── skills/<nama>/SKILL.md          # 30 skills, tiap skill = 1 folder + 1 SKILL.md (wajib)
│   └── scripts/, references/       # opsional per-skill (brainstorming punya)
├── references/                      # 7 shared checklist (dipakai banyak skill)
│   ├── accessibility-checklist.md
│   ├── definition-of-done.md
│   ├── observability-checklist.md
│   ├── orchestration-patterns.md
│   ├── performance-checklist.md
│   ├── security-checklist.md
│   └── testing-patterns.md
├── docs/
│   ├── CONSTRAINTS.md               # kanonikal (ganti root CONSTRAINTS.md)
│   ├── specs/active/                # spec aktif
│   └── specs/archive/               # spec selesai (todo 100%)
├── AGENTS.md
├── plugin.json
└── README.md
```

## Cara buat skill baru

```bash
# duplikasi skill terdekat sebagai template
cp -r skills/spec-driven-development skills/nama-baru
# edit skills/nama-baru/SKILL.md -> ganti name & description (harus == nama folder)
git add skills/nama-baru && git commit -m "feat: add nama-baru" && git push
# langsung: npx skills add dimsdeall/my-skills --skill nama-baru --list
```

## Commands — 6 CORE + 2 OPSIONAL (8)

**CORE — lifecycle SPEC → SHIP** (dipakai tiap fitur):

| Command | Fase | Skill(s) |
|---------|------|----------|
| `/spec` | SPEC — PRD (WHAT & WHY) | `brainstorming` → `idea-refine` → `interview-me` → `spec-driven-development` → `prd.md` |
| `/plan` | PLAN — impl plan (HOW) + tasks (ORDER) | `planning-and-task-breakdown` + `context-engineering` + `api/database` (kondisional) → `implementation-plan.md` + `tasks/plan.md` |
| `/build` (`/build auto`) | BUILD | `incremental-implementation` + `test-driven-development` |
| `/verify` | VERIFY | `debugging-and-error-recovery` + `security`/`perf`/`doubt`/`webapp-testing` (web opsional) |
| `/review` | REVIEW | `code-review-and-quality` + `code-simplification` + `documentation-and-adrs` |
| `/ship` | SHIP | `shipping-and-launch` + `ci-cd-and-automation` + `observability` + `git-workflow` |

**OPSIONAL — tidak termasuk lifecycle development, tapi tetap ada sebagai command:**

| Command | Kapan | Skill(s) |
|---------|-------|----------|
| `/constraints` | SETUP (sekali di awal / saat bar belum ada) | `constraint-driven-development` — interview 4Q → `CONSTRAINTS.md` + install tools + ratchets + guards |
| `/explain-code` | Kapan pun (read-only, tidak ubah kode) | `improve-codebase-architecture` (arsitektur) + `database-schema-designer` (skema) + `write-feature-docs` (fitur) — pilih a/b/c, bisa kombinasi |

File ada di `commands/*.toml` — format `skills` CLI (agenticskills.io) yang dipakai `npx skills add` untuk register command.

## Instal lokal (OpenCode / Hermes)

```bash
mkdir -p .opencode/skills
cp -r ~/projects/my-skills/skills/<nama> .opencode/skills/
```

## Lisensi

MIT — bebas pakai & modifikasi.
