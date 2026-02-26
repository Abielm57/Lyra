---
name: lyra-session-logs
description: "Cari dan analisis session logs percakapan lama menggunakan jq dan rg. Pakai kalau pemilik tanya tentang obrolan sebelumnya atau mau cek history."
homepage: https://github.com/Abielm57/Lyra
metadata: {"clawdbot":{"emoji":"📜","requires":{"bins":["jq","rg"]},"install":[{"id":"jq-rg","kind":"run","label":"Install jq dan ripgrep","run":"apt-get install -y jq ripgrep"}]}}
---

# LYRA Session Logs

Session logs ada di: `~/.openclaw/agents/<agentId>/sessions/`

## Cara Dapat Agent ID

Cek dari system prompt di bagian Runtime, nilai `agent=<id>`.

## Query Umum

### List semua session
```bash
for f in ~/.openclaw/agents/*/sessions/*.jsonl; do
  date=$(head -1 "$f" | jq -r '.timestamp' | cut -dT -f1)
  size=$(ls -lh "$f" | awk '{print $5}')
  echo "$date $size $(basename $f)"
done | sort -r
```

### Cari keyword di semua session
```bash
rg -l "keyword" ~/.openclaw/agents/*/sessions/*.jsonl
```

### Baca pesan user dari session tertentu
```bash
jq -r 'select(.message.role=="user") | .message.content[]? | select(.type=="text") | .text' SESSION.jsonl
```

### Cek total biaya session
```bash
jq -s '[.[] | .message.usage.cost.total // 0] | add' SESSION.jsonl
```

### Rekap biaya harian
```bash
for f in ~/.openclaw/agents/*/sessions/*.jsonl; do
  date=$(head -1 "$f" | jq -r '.timestamp' | cut -dT -f1)
  cost=$(jq -s '[.[] | .message.usage.cost.total // 0] | add' "$f")
  echo "$date $cost"
done | awk '{a[$1]+=$2} END {for(d in a) print d, "$"a[d]}' | sort -r
```

## Trigger

Pakai skill ini kalau pemilik tanya:
- "Kita pernah bahas apa kemarin?"
- "Kemarin aku minta apa ya?"
- "Recap obrolan kita minggu lalu dong"
- "Berapa biaya yang udah aku pakai?"
