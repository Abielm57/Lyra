---
name: lyra-ramadan
description: "Jadwal sholat 5 waktu Pasuruan via AlAdhan API. Reminder imsak, buka puasa, tarawih. Briefing Ramadan jam 04:30 WIB via openclaw cron. Gratis tanpa API key."
homepage: https://aladhan.com/prayer-times-api
metadata: {"clawdbot":{"emoji":"🌙","requires":{"bins":["curl"]},"install":[]}}
---

# LYRA Ramadan & Islamic Life

## API Jadwal Sholat

```bash
# Fetch jadwal sholat Pasuruan hari ini
curl -s "https://api.aladhan.com/v1/timingsByCity/$(date +%d-%m-%Y)?city=Pasuruan&country=Indonesia&method=11"
```

Method 11 = KEMENAG Indonesia. Field: Imsak, Fajr, Dhuhr, Asr, Maghrib, Isha.

## Cek Ramadan

```bash
# Cek bulan Hijriah — kalau month.number == 9, ini Ramadan
curl -s "https://api.aladhan.com/v1/gToH/$(date +%d-%m-%Y)" | jq '.data.hijri.month.number'
```

## Cron (via openclaw cron)

```bash
# Update jadwal sholat tiap hari jam 00:01
openclaw cron add --name "lyra:sholat-update" --schedule "1 0 * * *" \
  --prompt "Fetch jadwal sholat Pasuruan hari ini dari AlAdhan API method 11. Simpan ke memory."

# Briefing Ramadan jam 04:30 WIB (aktif saat Ramadan)
openclaw cron add --name "lyra:briefing-ramadan" --schedule "30 4 * * *" \
  --prompt "Cek apakah Ramadan. Kalau iya, kirim briefing pagi: hari ke-X Ramadan, jadwal sholat lengkap, ayat harian, semangat sahur."
```

## Notifikasi

**Imsak (20 menit sebelum):**
```
⏰ Imsak 20 menit lagi!
Imsak: [waktu] | Subuh: [waktu]
```

**Buka puasa (Maghrib):**
```
🌙 Alhamdulillah, waktunya berbuka!
"Dzahabaz zhoma-u wabtallatil uruuqu wa tsabatal ajru insyaa Allah"
```

**Briefing Ramadan:**
```
🌅 Hari ke-[X] Ramadan | [tanggal]
📖 "[ayat]" — QS. [surah]:[ayat]
🕌 Imsak [w] | Subuh [w] | Dzuhur [w] | Ashar [w] | Maghrib [w] | Isya [w]
```

## Command

```
!sholat     — jadwal sholat hari ini
!imsak      — menit lagi imsak
!buka       — menit lagi buka puasa
!puasa      — hari ke berapa Ramadan
!hijriah    — tanggal Hijriah
!doa [nama] — tampilkan doa
```
