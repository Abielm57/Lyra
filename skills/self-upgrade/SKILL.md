---
name: lyra-self-upgrade
description: "LYRA berkembang sendiri — deteksi gap, buat skill baru, belajar dari percakapan. Weekly review via openclaw cron tiap Minggu jam 20:00 WIB."
homepage: https://github.com/Abielm57/Lyra
metadata: {"clawdbot":{"emoji":"🔧","requires":{},"install":[]}}
---

# LYRA Self-Upgrade

## Cara Kerja

1. **Deteksi gap** — permintaan yang tidak ada skill-nya, atau pola > 3x
2. **Tanya izin** — "Mau aku buatin skill baru untuk ini?"
3. **Buat SKILL.md** dengan format OpenClaw frontmatter yang benar
4. **Test** — verifikasi bisa dijalankan
5. **Notif** — "Aku baru buat skill [nama], sekarang bisa [X]"

## Cron Weekly Review
```bash
openclaw cron add --name "lyra:weekly-review" --schedule "0 20 * * 0" \
  --prompt "Buat weekly self-review: skill yang dipakai, gap yang ditemukan, skill baru yang dibuat, saran minggu depan. Kirim ke Discord."
```

## Format Review
```
📊 Weekly Review LYRA — [tanggal]
✅ Berjalan baik: [skill X dipakai N kali]
⚠️ Gap: [yang belum bisa]
🆕 Skill baru: [nama] — [alasan]
💡 Saran: [rekomendasi]
```

## Batasan

LYRA tidak buat skill yang:
- Bypass aturan keamanan utama
- Akses data orang lain
- Modifikasi SOUL.md tanpa izin eksplisit
