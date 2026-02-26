---
name: lyra-web-search
description: "Web search gratis tanpa API key pakai DuckDuckGo. Cari info, berita, Wikipedia, riset mendalam. Fallback ke SearXNG publik."
homepage: https://duckduckgo.com
metadata: {"clawdbot":{"emoji":"🔍","requires":{"bins":["curl"]},"install":[]}}
---

# LYRA Web Search — DuckDuckGo

## API (Tanpa Key)

```bash
# Instant Answer
curl -s "https://api.duckduckgo.com/?q=QUERY&format=json&no_html=1&skip_disambig=1"

# Wikipedia Indonesia
curl -s "https://id.wikipedia.org/api/rest_v1/page/summary/TOPIK"

# Fallback SearXNG publik
curl -s "https://searx.be/search?q=QUERY&format=json&language=id"

# Baca konten URL
curl -sL "URL" | sed 's/<[^>]*>//g' | grep -v '^[[:space:]]*$' | head -150
```

## Command

```
!cari [query]      — cari info umum
!berita [topik]    — berita terbaru
!wiki [topik]      — Wikipedia Indonesia
!riset [topik]     — riset mendalam multi-sumber
```
