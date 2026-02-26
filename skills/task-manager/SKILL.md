---
name: lyra-task-manager
description: "To-do list lokal di ~/.lyra/tasks.json. Reminder deadline via openclaw cron jam 07:00 dan 13:00 WIB."
homepage: https://github.com/Abielm57/Lyra
metadata: {"clawdbot":{"emoji":"✅","requires":{},"install":[]}}
---

# LYRA Task Manager

Data: `~/.lyra/data/tasks.json`

## Cron
```bash
openclaw cron add --name "lyra:task-reminder" --schedule "0 7,13 * * *" \
  --prompt "Cek task di ~/.lyra/data/tasks.json yang due hari ini atau besok. Kirim reminder kalau ada."
```

## Command
```
!task                  — semua task aktif
!task tambah [desc]    — tambah task
!task selesai [id]     — tandai selesai
!task urgent           — prioritas tinggi / due hari ini
```

Natural language: "Lyra, ingatkan bayar hosting tanggal 25"

## Format
```
📋 Tasks

🔴 Due hari ini: [N]
• [id] [judul] ⚠️

🟡 In Progress:
• [id] [judul] — due [tanggal]

🟢 Belum mulai: [N]
```
