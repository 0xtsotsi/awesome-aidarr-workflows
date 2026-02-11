# local-websearch

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/stperic/local-websearch/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/stperic/local-websearch/SKILL.md)
> Category: Search & Research

---

## Description

Search the web using a self-hosted SearXNG metasearch engine. Aggregates Google, Brave, DuckDuckGo, and more without API keys.

**Homepage:** https://docs.searxng.org
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search the web using a self-hosted SearXNG metasearch engine. Aggregates Google, Brave, DuckDuckGo, and more without API keys.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run local-websearch`)
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
You are executing the local-websearch workflow. Use the following context:

Description: Search the web using a self-hosted SearXNG metasearch engine. Aggregates Google, Brave, DuckDuckGo, and more without API keys.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: local-websearch
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: https://docs.searxng.org
```

---

## Original Skill Content



# SearXNG Web Search

Privacy-respecting metasearch via your self-hosted SearXNG instance.

## When to use (trigger phrases)

Use this skill when the user asks:
- "search the web for..."
- "look up..." / "find information about..."
- "what is..." (when current info needed)
- "research..." / "search for..."
- "google..." (redirect to privacy-respecting search)

## Quick start

```bash
python3 ~/.clawdbot/skills/searxng/scripts/searxng_search.py "your query"
python3 ~/.clawdbot/skills/searxng/scripts/searxng_search.py "query" --count 10
python3 ~/.clawdbot/skills/searxng/scripts/searxng_search.py "query" --lang de
```

## Setup

Set `SEARXNG_URL` environment variable:
```bash
export SEARXNG_URL="http://your-searxng-host:8888"
```

## Flags

| Flag | Default | Description |
|------|---------|-------------|
| `-n`, `--count` | 5 | Results to return (1-20) |
| `-l`, `--lang` | auto | Language code (en, de, fr, es, etc.) |

## Output

Returns JSON:
```json
{
  "query": "search terms",
  "count": 5,
  "results": [
    {"title": "...", "url": "...", "description": "...", "engines": ["google", "brave"], "score": 1.5}
  ]
}
```

## Notes

- No API keys needed—SearXNG aggregates upstream engines
- Results include source engines for transparency
- Scores indicate relevance (higher = better)
- For news, add "news" to query or use `--lang` for regional results
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
