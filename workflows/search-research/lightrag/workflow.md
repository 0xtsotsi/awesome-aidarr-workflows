# lightrag

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ruslanlanket/lightrag/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ruslanlanket/lightrag/SKILL.md)
> Category: Search & Research

---

## Description

Search and manage knowledge bases using LightRAG API. Supports multiple servers, context-aware writing, and direct information retrieval. Use when the user wants to query a LightRAG-powered knowledge base or use it as context for tasks.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search and manage knowledge bases using LightRAG API. Supports multiple servers, context-aware writing, and direct information retrieval. Use when the user wants to query a LightRAG-powered knowledge base or use it as context for tasks.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run lightrag`)
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
You are executing the lightrag workflow. Use the following context:

Description: Search and manage knowledge bases using LightRAG API. Supports multiple servers, context-aware writing, and direct information retrieval. Use when the user wants to query a LightRAG-powered knowledge base or use it as context for tasks.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: lightrag
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# LightRAG Skill

This skill allows you to interact with one or more LightRAG API servers. You can perform queries in various modes (local, global, hybrid, mix, naive) and use the retrieved context for further processing.

## Configuration

The skill uses a configuration file at `~/.lightrag_config.json` to store server details.
Format:
```json
{
  "servers": {
    "alias1": {
      "url": "http://server1:9621",
      "api_key": "optional_key"
    },
    "alias2": {
      "url": "http://server2:9621",
      "api_key": "optional_key"
    }
  },
  "default_server": "alias1"
}
```

## Workflows

### 1. Direct Search
To find information, use `scripts/query_lightrag.py`.
Modes: `local`, `global`, `hybrid`, `mix`, `naive`.

### 2. Using Context for Writing
To use a knowledge base as context (e.g., for a test or article):
1. Run `query_lightrag.py` with the `--only-context` flag.
2. Pass the resulting context to your writing task/model.

## Reference
See [API_DOCS.md](references/API_DOCS.md) for endpoint details.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
