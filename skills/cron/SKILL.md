---
name: lyra-cron
description: "Panduan fundamental openclaw cron untuk LYRA. Syntax baku, cara handle error, auto-adaptasi saat OpenClaw update. Selalu baca ini sebelum buat atau edit cron job apapun."
homepage: https://docs.openclaw.ai/cli/cron
metadata: {"clawdbot":{"emoji":"⏰","requires":{"bins":["openclaw"]},"install":[]}}
---

# LYRA Cron — Panduan Fundamental

## WAJIB DIBACA SEBELUM BUAT CRON APAPUN

Sebelum buat cron job, selalu cek syntax terbaru:
```bash
openclaw cron add --help
```

Jangan pernah asumsikan syntax — selalu verifikasi dulu.

---

## Syntax Baku (Verified OpenClaw 2026.2.25)

```bash
openclaw cron add \
  --name "namespace:jobname" \
  --cron "CRON_EXPRESSION" \
  --tz "Asia/Jakarta" \
  --message "Isi perintah untuk LYRA" \
  --announce
```

### Flag Penting

| Flag | Fungsi | Catatan |
|------|--------|---------|
| `--name` | Nama unik job | Format: `namespace:nama` |
| `--cron` | Jadwal cron 5-field | ⚠️ BUKAN `--schedule` |
| `--tz` | Timezone | Selalu `Asia/Jakarta` untuk WIB |
| `--message` | Perintah ke LYRA | ⚠️ BUKAN `--prompt` |
| `--announce` | Kirim hasil ke chat | Selalu pakai ini |
| `--every` | Interval (10m, 1h) | Alternatif `--cron` |
| `--at` | Jalankan sekali di waktu tertentu | ISO format |
| `--disabled` | Buat tapi jangan aktifkan | |
| `--description` | Deskripsi job | Opsional tapi recommended |

### ⚠️ Flag yang TIDAK ADA (jangan pakai)
- `--schedule` → gunakan `--cron`
- `--prompt` → gunakan `--message`

---

## Cron Expression (WIB = UTC+7)

```
┌─── menit (0-59)
│ ┌─── jam (0-23) dalam WIB karena --tz Asia/Jakarta
│ │ ┌─── hari bulan (1-31)
│ │ │ ┌─── bulan (1-12)
│ │ │ │ ┌─── hari minggu (0=Minggu, 1=Senin ... 6=Sabtu)
│ │ │ │ │
* * * * *
```

Contoh:
```
"1 0 * * *"      → tiap hari jam 00:01 WIB
"30 4 * * *"     → tiap hari jam 04:30 WIB
"0 7 * * *"      → tiap hari jam 07:00 WIB
"*/30 7-23 * * *"→ tiap 30 menit antara jam 07-23 WIB
"0 7,13 * * *"   → jam 07:00 dan 13:00 WIB tiap hari
"0 20 * * 0"     → Minggu jam 20:00 WIB
"0 23 * * *"     → tiap hari jam 23:00 WIB
"0 9 * * 1"      → Senin jam 09:00 WIB
"0 9 1 * *"      → tanggal 1 tiap bulan jam 09:00 WIB
```

---

## Operasi Cron

```bash
openclaw cron list              # lihat semua cron jobs
openclaw cron list --json       # output JSON
openclaw cron status            # status scheduler
openclaw cron run <id>          # jalankan sekarang (debug)
openclaw cron runs <id>         # history runs
openclaw cron enable <id>       # aktifkan job
openclaw cron disable <id>      # nonaktifkan sementara
openclaw cron edit <id> --message "pesan baru"  # edit job
openclaw cron rm <id>           # hapus job permanen
```

---

## Cron Jobs LYRA yang Aktif

| Name | Schedule | Fungsi |
|------|----------|--------|
| `lyra:sholat-update` | `1 0 * * *` | Update jadwal sholat Pasuruan tiap hari |
| `lyra:briefing-ramadan` | `30 4 * * *` | Briefing Ramadan pagi (aktif saat Ramadan) |
| `lyra:briefing-pagi` | `0 7 * * *` | Briefing pagi normal |
| `lyra:email-check` | `*/30 7-23 * * *` | Cek email baru tiap 30 menit |
| `lyra:task-reminder` | `0 7,13 * * *` | Reminder task due |
| `lyra:weekly-review` | `0 20 * * 0` | Weekly self-review Minggu malam |
| `lyra:memory-update` | `0 23 * * *` | Update MEMORY.md tiap malam |

---

## Cara Tambah Cron Job Baru

Kalau ada skill baru yang butuh jadwal:

```bash
# 1. Cek syntax terbaru dulu
openclaw cron add --help

# 2. Cek apakah nama sudah ada
openclaw cron list

# 3. Kalau nama sudah ada, edit saja
openclaw cron edit <id> --message "pesan baru"

# 4. Kalau belum ada, buat baru
openclaw cron add --name "lyra:nama-baru" --cron "0 8 * * *" --tz "Asia/Jakarta" --message "Perintah ke LYRA" --announce
```

---

## Auto-Adaptasi Saat OpenClaw Update

Kalau setelah update command cron error:

```bash
# Langkah 1: cek help terbaru
openclaw cron --help
openclaw cron add --help

# Langkah 2: identifikasi flag yang berubah
# Langkah 3: update syntax dan coba lagi
# Langkah 4: update MEMORY.md dengan syntax baru
```

**Prinsip:** Jangan pernah hardcode asumsi syntax. Selalu verifikasi dari `--help` kalau ada error.

---

## Troubleshoot

| Error | Kemungkinan Penyebab | Solusi |
|-------|---------------------|--------|
| `unknown option '--schedule'` | Pakai flag lama | Ganti dengan `--cron` |
| `unknown option '--prompt'` | Pakai flag lama | Ganti dengan `--message` |
| `error: gateway timeout` | Gateway tidak jalan | Jalankan dari terminal lokal, bukan dari dalam session LYRA |
| Job tidak jalan | Scheduler mati | Cek `openclaw cron status` |
| Job tidak jalan di waktu yang tepat | Timezone salah | Pastikan `--tz "Asia/Jakarta"` |

---

## Tambah Cron dari Dalam Chat LYRA

Kalau pemilik minta jadwal sesuatu dari Discord, LYRA buat cron via bash tool:

```bash
bash command:"openclaw cron add --name 'lyra:nama' --cron '0 8 * * *' --tz 'Asia/Jakarta' --message 'Perintah' --announce"
```

Kalau error, langsung jalankan `openclaw cron add --help` dan sesuaikan.
