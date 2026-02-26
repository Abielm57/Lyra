---
name: lyra-prompt-engineering
description: "Panduan prompt engineering untuk AI models: LLM, image generators, video. Teknik: chain-of-thought, few-shot, system prompts, output format. Pakai saat pemilik mau improve output AI."
homepage: https://github.com/Abielm57/Lyra
metadata: {"clawdbot":{"emoji":"✍️","requires":{},"install":[]}}
---

# LYRA Prompt Engineering

## Struktur Dasar LLM

```
[Role/Konteks] + [Task] + [Constraint] + [Output Format]
```

## Teknik Utama

### Role Prompting
```
"Kamu adalah senior developer Python dengan 10 tahun pengalaman.
Review kode ini untuk security vulnerabilities: [kode]"
```

### Chain-of-Thought
```
"Selesaikan ini step by step sebelum kasih jawaban final: [masalah]"
```

### Few-Shot
```
"Contoh input: [x] → output: [y]
Contoh input: [a] → output: [b]
Sekarang: input: [c] → output: ?"
```

### Output Format
```
"Return sebagai JSON array dengan field: name, status, priority.
Hanya return JSON, tanpa penjelasan."
```

## Template Siap Pakai

### Code Review
```
Review kode [bahasa] ini untuk:
1. Bug dan logic error
2. Security issues
3. Performance
4. Best practices

Kode: [kode]

Format: issue | baris | severity (high/medium/low) | solusi
```

### Generate Kode
```
Buat [bahasa] function yang:
- Input: [deskripsi input]
- Output: [deskripsi output]
- Constraint: [batasan]
- Include: error handling, comments, docstring
```

### Image Generation
```
[Subject detail], [setting], [lighting], [art style], [composition], [quality keywords]
Negative: blurry, distorted, low quality, watermark
```

## Kesalahan Umum

| Kesalahan | Masalah | Fix |
|-----------|---------|-----|
| Terlalu vague | Output tidak konsisten | Tambah spesifik |
| Terlalu panjang | Model kehilangan fokus | Prioritaskan info penting |
| Tanpa format | Output berantakan | Specify format output |
| Tanpa contoh | Ekspektasi tidak jelas | Tambah few-shot |

## Trigger

Pakai skill ini saat pemilik tanya:
- "Gimana cara prompt yang bagus?"
- "Output AI-nya jelek, kenapa?"
- "Bantu aku bikin system prompt"
- "Cara bikin image prompt yang detail?"
