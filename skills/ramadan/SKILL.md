---
name: lyra-ramadan
description: "Jadwal sholat Pasuruan via AlAdhan API. Reminder imsak, buka puasa, briefing Ramadan. Gratis tanpa API key."
homepage: https://aladhan.com/prayer-times-api
metadata: {"clawdbot":{"emoji":"🌙","requires":{"bins":["curl"]},"install":[]}}
---

# LYRA Ramadan & Sholat

## API
```bash
# Jadwal sholat hari ini
curl -s "https://api.aladhan.com/v1/timingsByCity/$(date +%d-%m-%Y)?city=Pasuruan&country=Indonesia&method=11"

# Cek Ramadan (month.number == 9 = Ramadan)
curl -s "https://api.aladhan.com/v1/gToH/$(date +%d-%m-%Y)" | jq '.data.hijri.month.number'
```

## Notifikasi

**Imsak -20 menit:** `⏰ Imsak 20 menit lagi! [waktu]`

**Sholat:** `🕌 Waktunya sholat [nama] — [waktu] WIB`

**Buka puasa:**
```
🌙 Alhamdulillah, waktunya berbuka! [waktu]
"Dzahabaz zhoma-u wabtallatil uruuqu..."
```

**Briefing Ramadan (04:30):**
```
🌅 Hari ke-[X] Ramadan
📖 [ayat] — QS. [surah]:[ayat]
🕌 Imsak [w] Subuh [w] Dzuhur [w] Ashar [w] Maghrib [w] Isya [w]
```

## Command
```
!sholat   — jadwal hari ini
!imsak    — menit lagi imsak
!buka     — menit lagi buka
!puasa    — hari ke berapa Ramadan
!hijriah  — tanggal Hijriah
!doa [x]  — tampilkan doa
```
