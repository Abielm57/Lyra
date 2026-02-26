---
name: lyra-daily-briefing
description: "Briefing harian otomatis via openclaw cron. Normal 07:00 WIB, Ramadan 04:30 WIB. Isi: sholat, cuaca, email, task, agenda."
homepage: https://github.com/Abielm57/Lyra
metadata: {"clawdbot":{"emoji":"🌅","requires":{"bins":["curl"]},"suggests":["lyra-ramadan","lyra-email","lyra-task-manager"],"install":[]}}
---

# LYRA Daily Briefing

## Cuaca (Tanpa API Key)
```bash
curl -s "https://wttr.in/Pasuruan?format=3"
# Output: Pasuruan: ⛅️ +29°C
```

## Format Pagi Normal
```
🌅 Selamat pagi! [Hari, DD MMM YYYY]

🕌 Sholat: Subuh [w] | Dzuhur [w] | Ashar [w] | Maghrib [w] | Isya [w]
🌤️ Cuaca: [wttr.in]
📧 Email: [N] urgent
📋 Task: [N] due hari ini
```

## Format Ramadan (04:30)
```
🌙 Hari ke-[X] Ramadan
📖 "[ayat]" — QS. [surah]:[ayat]
🕌 Imsak [w] | Subuh [w] | Maghrib/Buka [w]
```
