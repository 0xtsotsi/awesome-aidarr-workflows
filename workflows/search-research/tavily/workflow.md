# tavily

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/arun-8687/tavily-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/arun-8687/tavily-search/SKILL.md)
> Category: Search & Research

---

## Description

AI-optimized web search via Tavily API. Returns concise, relevant results for AI agents.

**Homepage:** https://tavily.com
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
AI-optimized web search via Tavily API. Returns concise, relevant results for AI agents.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tavily`)
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
You are executing the tavily workflow. Use the following context:

Description: AI-optimized web search via Tavily API. Returns concise, relevant results for AI agents.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tavily
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: https://tavily.com
```

---

## Original Skill Content



# Tavily Search

AI-optimized web search using Tavily API. Designed for AI agents - returns clean, relevant content.

## Search

```bash
node {baseDir}/scripts/search.mjs "query"
node {baseDir}/scripts/search.mjs "query" -n 10
node {baseDir}/scripts/search.mjs "query" --deep
node {baseDir}/scripts/search.mjs "query" --topic news
```

## Options

- `-n <count>`: Number of results (default: 5, max: 20)
- `--deep`: Use advanced search for deeper research (slower, more comprehensive)
- `--topic <topic>`: Search topic - `general` (default) or `news`
- `--days <n>`: For news topic, limit to last n days

## Extract content from URL

```bash
node {baseDir}/scripts/extract.mjs "https://example.com/article"
```

Notes:
- Needs `TAVILY_API_KEY` from https://tavily.com
- Tavily is optimized for AI - returns clean, relevant snippets
- Use `--deep` for complex research questions
- Use `--topic news` for current events

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
