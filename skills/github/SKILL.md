---
name: lyra-github
description: "GitHub via gh CLI. Cari repo, cek notifikasi, lihat issues/PR, monitor repo favorit, clone, buat repo baru."
homepage: https://cli.github.com
metadata: {"clawdbot":{"emoji":"🐙","requires":{"bins":["gh"]},"install":[{"id":"gh-apt","kind":"run","label":"Install gh CLI","run":"curl -fsSL https://cli.github.com/packages/githubcli-archive-keyring.gpg | sudo dd of=/usr/share/keyrings/githubcli-archive-keyring.gpg && echo \"deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/githubcli-archive-keyring.gpg] https://cli.github.com/packages stable main\" | sudo tee /etc/apt/sources.list.d/github-cli.list > /dev/null && sudo apt update && sudo apt install gh -y"}]}}
---

# LYRA GitHub

## Setup
```bash
gh auth login   # ikuti wizard, pilih browser atau paste token
gh auth status  # verifikasi
```

## Operasi
```bash
gh search repos "QUERY" --sort stars
gh repo view user/repo
gh issue list --repo user/repo
gh pr list --repo user/repo
gh api notifications
gh repo clone user/repo
gh repo create nama --public
```

## Command
```
!gh cari [query]    — cari repo
!gh trending        — trending hari ini
!gh repo [user/x]   — info repo
!gh issues [user/x] — lihat issues
!gh notif           — notifikasi GitHub
!gh clone [user/x]  — clone repo (konfirmasi dulu)
```
