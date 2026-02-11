# qmd

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/qmd/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/qmd/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Local search/indexing CLI (BM25 + vectors + rerank) with MCP mode.

**Homepage:** https://tobi.lutke.com
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Local search/indexing CLI (BM25 + vectors + rerank) with MCP mode.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run qmd`)
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
You are executing the qmd workflow. Use the following context:

Description: Local search/indexing CLI (BM25 + vectors + rerank) with MCP mode.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: qmd
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: https://tobi.lutke.com
```

---

## Original Skill Content



# qmd

Use `qmd` to index local files and search them.

Indexing
- Add collection: `qmd collection add /path --name docs --mask "**/*.md"`
- Update index: `qmd update`
- Status: `qmd status`

Search
- BM25: `qmd search "query"`
- Vector: `qmd vsearch "query"`
- Hybrid: `qmd query "query"`
- Get doc: `qmd get docs/path.md:10 -l 40`

Notes
- Embeddings/rerank use Ollama at `OLLAMA_URL` (default `http://localhost:11434`).
- Index lives under `~/.cache/qmd` by default.
- MCP mode: `qmd mcp`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
