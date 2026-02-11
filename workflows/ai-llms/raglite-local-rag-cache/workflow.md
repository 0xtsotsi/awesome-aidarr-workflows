# raglite-local-rag-cache

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/virajsanghvi1/raglite-local-rag-cache/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/virajsanghvi1/raglite-local-rag-cache/SKILL.md)
> Category: AI & LLMs

---

## Description

Local-first RAG cache: distill docs into structured Markdown, then index/query with Chroma + hybrid search (vector + keyword).

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Local-first RAG cache: distill docs into structured Markdown, then index/query with Chroma + hybrid search (vector + keyword).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run raglite-local-rag-cache`)
**Workflow:** Execute skill logic with context from AiDarr's ATLAS memory

### T - Tools
Required tools (add as needed):
- HTTP requests (for API calls)
- Memory system (ATLAS for persistence)
- Context retrieval (from GOTCHA workspace)

### C - Context
Required context sources:
- User preferences from ATLAS memory
- Relevant documents from workspace
- Historical execution data

### H - Hard Prompts

```prompt
You are executing the raglite-local-rag-cache workflow. Use the following context:

Description: Local-first RAG cache: distill docs into structured Markdown, then index/query with Chroma + hybrid search (vector + keyword).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: raglite-local-rag-cache
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# RAGLite — a local RAG cache (not a memory replacement)

RAGLite is a **local-first RAG cache**.

It does **not** replace model memory or chat context. It gives your agent a durable place to store and retrieve information the model wasn’t trained on — especially useful for **local/private knowledge** (school work, personal notes, medical records, internal runbooks).

## Why it’s better than “paid RAG” / knowledge bases (for many use cases)

- **Local-first privacy:** keep sensitive data on your machine/network.
- **Open-source building blocks:** **Chroma** 🧠 + **ripgrep** ⚡ — no managed vector DB required.
- **Compression-before-embeddings:** distill first → less fluff/duplication → cheaper prompts + more reliable retrieval.
- **Auditable artifacts:** the distilled Markdown is human-readable and version-controllable.

If you later outgrow local, you can swap in a hosted DB — but you often don’t need to.

## What it does

### 1) Condense ✍️
Turns docs into structured Markdown outputs (low fluff, more “what matters”).

### 2) Index 🧠
Embeds the distilled outputs into a **Chroma** collection (one DB, many collections).

### 3) Query 🔎
Hybrid retrieval:
- vector similarity via Chroma
- keyword matches via ripgrep (`rg`)

## Default engine

This skill defaults to **OpenClaw** 🦞 for condensation unless you pass `--engine` explicitly.

## Prereqs

- **Python 3.11+**
- For indexing/query:
  - Chroma server reachable (default `http://127.0.0.1:8100`)
- For hybrid keyword search:
  - `rg` installed (`brew install ripgrep`)
- For OpenClaw engine:
  - OpenClaw Gateway `/v1/responses` reachable
  - `OPENCLAW_GATEWAY_TOKEN` set if your gateway requires auth

## Install (skill runtime)

This skill installs RAGLite into a skill-local venv:

```bash
./scripts/install.sh
```

It installs from GitHub:
- `git+https://github.com/VirajSanghvi1/raglite.git@main`

## Usage

### One-command pipeline (recommended)

```bash
./scripts/raglite.sh run /path/to/docs \
  --out ./raglite_out \
  --collection my-docs \
  --chroma-url http://127.0.0.1:8100 \
  --skip-existing \
  --skip-indexed \
  --nodes
```

### Query

```bash
./scripts/raglite.sh query ./raglite_out \
  --collection my-docs \
  --top-k 5 \
  --keyword-top-k 5 \
  "rollback procedure"
```

## Outputs (what gets written)

In `--out` you’ll see:
- `*.tool-summary.md`
- `*.execution-notes.md`
- optional: `*.outline.md`
- optional: `*/nodes/*.md` plus per-doc `*.index.md` and a root `index.md`
- metadata in `.raglite/` (cache, run stats, errors)

## Troubleshooting

- **Chroma not reachable** → check `--chroma-url`, and that Chroma is running.
- **No keyword results** → install ripgrep (`rg --version`).
- **OpenClaw engine errors** → ensure gateway is up and token env var is set.

## Pitch (for ClawHub listing)

RAGLite is a **local RAG cache** for repeated lookups.

When you (or your agent) keep re-searching for the same non-training data — local notes, school work, medical records, internal docs — RAGLite gives you a private, auditable library:

1) **Distill** to structured Markdown (compression-before-embeddings)
2) **Index** locally into Chroma
3) **Query** with hybrid retrieval (vector + keyword)

It doesn’t replace memory/context — it’s the place to store what you need again.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
