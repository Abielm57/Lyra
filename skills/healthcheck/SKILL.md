---
name: lyra-healthcheck
description: "Security audit dan hardening host Ubuntu yang menjalankan OpenClaw. Cek firewall, SSH, update status, versi OpenClaw. Pakai openclaw cron untuk audit berkala."
homepage: https://github.com/Abielm57/Lyra
metadata: {"clawdbot":{"emoji":"🔒","requires":{},"install":[]}}
---

# LYRA Healthcheck

## Quick Audit

```bash
openclaw security audit
openclaw security audit --deep
openclaw update status
```

## Host Checks (Read-Only)

```bash
uname -a                          # OS info
ss -ltnup                         # port yang listening
ufw status                        # firewall status
```

## Cron Berkala

```bash
# Healthcheck tiap Senin jam 09:00 WIB
openclaw cron add --name "lyra:healthcheck" --schedule "0 9 * * 1" \
  --prompt "Jalankan: openclaw security audit dan openclaw update status. Laporkan hasilnya. Kalau ada issue, kasih rekomendasi perbaikan."
```

## Aturan

- Tunjukkan plan dulu sebelum eksekusi
- Minta konfirmasi sebelum: ubah firewall, install package, ubah SSH config
- Jangan klaim OpenClaw bisa ubah host firewall/SSH — dia tidak bisa
- Kalau tidak ada sudo, cukup rekomendasikan saja

## Trigger

Pakai skill ini kalau pemilik tanya:
- "Cek keamanan server dong"
- "Ada update OpenClaw?"
- "Port apa yang terbuka?"
- "Auditkan sistem aku"
