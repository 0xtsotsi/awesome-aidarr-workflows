# qmd-cli

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dpaluy/qmd-cli/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dpaluy/qmd-cli/SKILL.md)
> Category: Search & Research

---

## Description

Search and retrieve markdown documents from local knowledge bases using qmd. Supports BM25 keyword search, vector semantic search, and hybrid search with LLM re-ranking. Use for querying indexed notes, documentation, meeting transcripts, and any markdown-based knowledge. Requires qmd CLI installed (bun install -g https://github.com/tobi/qmd).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search and retrieve markdown documents from local knowledge bases using qmd. Supports BM25 keyword search, vector semantic search, and hybrid search with LLM re-ranking. Use for querying indexed notes, documentation, meeting transcripts, and any markdown-based knowledge. Requires qmd CLI installed (bun install -g https://github.com/tobi/qmd).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run qmd-cli`)
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
You are executing the qmd-cli workflow. Use the following context:

Description: Search and retrieve markdown documents from local knowledge bases using qmd. Supports BM25 keyword search, vector semantic search, and hybrid search with LLM re-ranking. Use for querying indexed notes, documentation, meeting transcripts, and any markdown-based knowledge. Requires qmd CLI installed (bun install -g https://github.com/tobi/qmd).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: qmd-cli
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# QMD - Local Markdown Search

Search and retrieve documents from locally indexed markdown knowledge bases.

## Installation

```bash
bun install -g https://github.com/tobi/qmd
```

## Setup

```bash
# Add a collection
qmd collection add ~/notes --name notes --mask "**/*.md"

# Generate embeddings (required for vsearch/query)
qmd embed
```

## Usage Rules

**Always use `--json` flag** for structured output when invoking qmd commands.

## Search Commands

### search (BM25 keyword search - fast)

```bash
qmd search "authentication flow" --json
qmd search "error handling" --json -n 10
qmd search "config" --json -c notes
```

### vsearch (vector semantic search)

```bash
qmd vsearch "how does login work" --json
qmd vsearch "authentication best practices" --json -n 20
```

### query (hybrid with LLM re-ranking - best quality)

```bash
qmd query "implementing user auth" --json
qmd query "deployment process" --json --min-score 0.5
```

### Search Options

| Option | Description |
|--------|-------------|
| `-n NUM` | Number of results (default: 5, or 20 with --json) |
| `-c, --collection NAME` | Restrict to specific collection |
| `--min-score NUM` | Minimum score threshold |
| `--full` | Return complete document content in results |
| `--all` | Return all matches |

## Retrieval Commands

### get (single document)

```bash
qmd get docs/guide.md --json
qmd get "#a1b2c3" --json
qmd get notes/meeting.md:50 -l 100 --json
```

### multi-get (multiple documents)

```bash
qmd multi-get "docs/*.md" --json
qmd multi-get "api.md, guide.md, #abc123" --json
qmd multi-get "notes/**/*.md" --json --max-bytes 20480
```

## Maintenance Commands

```bash
qmd update              # Re-index changed files
qmd status              # Check index health
qmd collection list     # List all collections
```

## Search Mode Selection

| Mode | Speed | Quality | Best For |
|------|-------|---------|----------|
| search | Fast | Good | Exact keywords, known terms |
| vsearch | Medium | Better | Conceptual queries, synonyms |
| query | Slow | Best | Complex questions, uncertain terms |

**Performance note:** `vsearch` and `query` have ~1 minute cold start latency for vector initialization. Prefer `search` for interactive use.

## MCP Server

qmd can run as an MCP server for direct integration:

```bash
qmd mcp
```

Exposes tools: `qmd_search`, `qmd_vsearch`, `qmd_query`, `qmd_get`, `qmd_multi_get`, `qmd_status`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
