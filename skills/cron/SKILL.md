---
name: lyra-cron
description: "Panduan fundamental openclaw cron. Syntax baku, auto-adaptasi saat update. SELALU baca ini sebelum buat atau edit cron job apapun."
homepage: https://docs.openclaw.ai/cli/cron
metadata: {"clawdbot":{"emoji":"⏰","requires":{"bins":["openclaw"]},"install":[]}}
---

# LYRA Cron — Fundamental

## WAJIB: Cek Syntax Sebelum Buat Cron

```bash
openclaw cron add --help
```

Jangan asumsikan syntax — selalu verifikasi dari --help kalau ada error.

## Syntax Baku (Verified v2026.2.25)

```bash
openclaw cron add \
  --name "lyra:jobname" \
  --cron "* * * * *" \
  --tz "Asia/Jakarta" \
  --message "Perintah ke LYRA" \
  --announce
```

| Flag | ✅ Benar | ❌ Salah |
|------|---------|---------|
| Jadwal | `--cron` | `--schedule` |
| Perintah | `--message` | `--prompt` |
| Timezone | `--tz "Asia/Jakarta"` | — |
| Notif | `--announce` | — |

## Cron Expression (WIB)

```
"1 0 * * *"        → 00:01 WIB tiap hari
"30 4 * * *"       → 04:30 WIB tiap hari
"0 7 * * *"        → 07:00 WIB tiap hari
"*/30 7-23 * * *"  → tiap 30 menit jam 07-23
"0 7,13 * * *"     → 07:00 dan 13:00 WIB
"0 20 * * 0"       → Minggu 20:00 WIB
"0 23 * * *"       → 23:00 WIB tiap hari
```

## Operasi

```bash
openclaw cron list                          # lihat semua job
openclaw cron run <id>                      # test jalankan sekarang
openclaw cron edit <id> --message "baru"   # edit job
openclaw cron disable <id>                  # nonaktifkan
openclaw cron rm <id>                       # hapus
```

## Cron Jobs LYRA Aktif

| Name | Schedule | Fungsi |
|------|----------|--------|
| `lyra:sholat` | `1 0 * * *` | Update jadwal sholat |
| `lyra:briefing-ramadan` | `30 4 * * *` | Briefing Ramadan |
| `lyra:briefing-pagi` | `0 7 * * *` | Briefing pagi |
| `lyra:email-check` | `*/30 7-23 * * *` | Cek email |
| `lyra:task-reminder` | `0 7,13 * * *` | Reminder task |
| `lyra:memory-update` | `0 23 * * *` | Update MEMORY.md |
| `lyra:weekly-review` | `0 20 * * 0` | Weekly review |

## Kalau Error Setelah OpenClaw Update

1. `openclaw cron add --help` — lihat flag terbaru
2. Sesuaikan command dengan flag yang ada
3. Update MEMORY.md dengan syntax baru
4. Jangan pakai flag yang tidak ada di --help
