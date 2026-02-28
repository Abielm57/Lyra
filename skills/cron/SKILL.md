---
name: lyra-cron
description: "Panduan fundamental openclaw cron. Selalu baca ini sebelum buat atau edit cron job. Auto-adaptasi saat OpenClaw update."
homepage: https://docs.openclaw.ai/cli/cron
metadata: {"clawdbot":{"emoji":"⏰","requires":{"bins":["openclaw"]},"install":[]}}
---

# LYRA Cron

## WAJIB: Cek Syntax Dulu
```bash
openclaw cron add --help
```

## Syntax Baku (v2026.2.25)
```bash
openclaw cron add --name "lyra:nama" --cron "* * * * *" --tz "Asia/Jakarta" --message "perintah" --announce
```

| ✅ Benar | ❌ Salah |
|---------|---------|
| `--cron` | `--schedule` |
| `--message` | `--prompt` |

## Jadwal Umum WIB
```
"0 7 * * *"       → 07:00 tiap hari
"*/30 7-23 * * *" → tiap 30 menit jam 07-23
"0 7,13 * * *"    → 07:00 dan 13:00
"0 20 * * 0"      → Minggu 20:00
"0 23 * * *"      → 23:00 tiap hari
```

## Operasi
```bash
openclaw cron list              # lihat semua
openclaw cron run <id>          # test sekarang
openclaw cron edit <id> --message "baru"
openclaw cron disable <id>
openclaw cron rm <id>
```

## Kalau Error Setelah Update
1. Jalankan `openclaw cron add --help`
2. Sesuaikan flag dengan output terbaru
3. Update MEMORY.md dengan syntax baru
