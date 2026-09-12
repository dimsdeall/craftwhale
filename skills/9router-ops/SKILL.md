---
name: 9router-ops
description: Operasional 9Router gateway milik Dimas (PM2, build, update). Use when updating, restarting, or debugging 9Router at https://9router.dimsdeall.my.id.
---

# 9Router Ops

Skill operasional 9Router — gateway AI routing di `https://9router.dimsdeall.my.id`.

## Stack

- Repo: `https://github.com/decolua/9router` (clone di `~/9router`)
- PM2: `pm2 list` → `9router` (fork, `npm start`, port `20127`)
- Default model: `Combi-hermes` (combo 4 model, strategy fallback)

## Update Flow (v0.5.69 → v0.5.75 pattern)

```bash
cd ~/9router
git stash push -m "pre-update local patch"  # amankan layout patch lokal
git pull origin master
npm install
npm run build
pm2 restart 9router && pm2 save
curl -s http://127.0.0.1:20127/api/version  # expect hasUpdate:false
```

## Health Checks

- `pm2 info 9router` — status online, uptime reset setelah restart
- `pm2 logs 9router --lines 30 --nostream` — cek `Ready in ...` + `[DB] Driver`
- `GET /v1/models` — 19 models, `Combi-hermes` ada

## Gotchas

- Lokal ada patch `src/app/globals.css` + `layout.js` + `Inter-Variable.woff2` → wajib stash sebelum pull.
- Build butuh Node 26 (Hermes) / Node 24 untuk ECC — cek `nvm use`.
