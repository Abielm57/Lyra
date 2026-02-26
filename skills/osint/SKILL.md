---
name: lyra-osint
description: "Cek kebocoran data pribadi pemilik — email via HaveIBeenPwned, password via PwnedPasswords (k-Anonymity), jejak digital. Monitor bulanan via openclaw cron."
homepage: https://haveibeenpwned.com/API/v3
metadata: {"clawdbot":{"emoji":"🕵️","requires":{"bins":["curl"]},"install":[]}}
---

# LYRA OSINT & Privacy

## Cek Email Bocor
```bash
# Butuh API key gratis dari haveibeenpwned.com/API/Key
curl -s "https://haveibeenpwned.com/api/v3/breachedaccount/EMAIL" \
  -H "hibp-api-key: API_KEY" -H "user-agent: LYRA"
```

## Cek Password (Tanpa kirim password ke server)
```bash
# k-Anonymity: hanya 5 karakter pertama SHA1 yang dikirim
HASH=$(echo -n "PASSWORD" | sha1sum | cut -c1-5 | tr a-z A-Z)
curl -s "https://api.pwnedpasswords.com/range/$HASH"
```

## Cron Monitor Bulanan
```bash
openclaw cron add --name "lyra:privacy-check" --schedule "0 9 1 * *" \
  --prompt "Cek kebocoran data email pemilik via HaveIBeenPwned. Alert kalau ada breach baru."
```

## Command
```
!osint email [x]  — cek email bocor
!osint audit      — audit privacy lengkap
!osint laporan    — laporan risiko lengkap
```

## Format Laporan
```
🔍 Privacy Report — [tanggal]
📧 [email]: 🔴 BOCOR / 🟢 AMAN
[Kalau bocor:]
• [breach name] — [tanggal] — Data: [tipe]
✅ Rekomendasi: ganti password, aktifkan 2FA
```
