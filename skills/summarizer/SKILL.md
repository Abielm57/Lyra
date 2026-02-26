---
name: lyra-summarizer
description: "Ringkas artikel web, YouTube (yt-dlp), PDF, teks panjang. Output selalu bahasa Indonesia."
homepage: https://github.com/Abielm57/Lyra
metadata: {"clawdbot":{"emoji":"📄","requires":{"bins":["curl"]},"suggests":["yt-dlp"],"install":[{"id":"yt-dlp","kind":"run","label":"Install yt-dlp","run":"pip3 install yt-dlp --break-system-packages"}]}}
---

# LYRA Summarizer

## Fetch Artikel
```bash
curl -sL "URL" | sed 's/<[^>]*>//g' | grep -v '^[[:space:]]*$' | head -150
```

## YouTube Transcript
```bash
yt-dlp --write-auto-sub --sub-lang id,en --skip-download --sub-format vtt -o "/tmp/transcript" "URL_YT"
```

## Command
```
!ringkas [URL/teks]  — ringkas konten
!tldr [URL]          — 3 poin utama
!jelasin [URL/teks]  — ringkas + jelaskan untuk pemula
```

## Format Output
```
📄 Intinya: [1 kalimat]
• [poin 1]
• [poin 2]
• [poin 3]
Catatan: [relevansi untuk pemilik]
```
