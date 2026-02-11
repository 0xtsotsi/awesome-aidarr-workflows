# perplexity

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/zats/perplexity/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/zats/perplexity/SKILL.md)
> Category: AI & LLMs

---

## Description

Search the web with AI-powered answers via Perplexity API. Returns grounded responses with citations. Supports batch queries.

**Homepage:** https://docs.perplexity.ai
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search the web with AI-powered answers via Perplexity API. Returns grounded responses with citations. Supports batch queries.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run perplexity`)
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
You are executing the perplexity workflow. Use the following context:

Description: Search the web with AI-powered answers via Perplexity API. Returns grounded responses with citations. Supports batch queries.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: perplexity
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: https://docs.perplexity.ai
```

---

## Original Skill Content



# Perplexity Search

AI-powered web search that returns grounded answers with citations.

## Search

Single query:
```bash
node {baseDir}/scripts/search.mjs "what's happening in AI today"
```

Multiple queries (batch):
```bash
node {baseDir}/scripts/search.mjs "What is Perplexity?" "Latest AI news" "Best coffee in NYC"
```

## Options

- `--json`: Output raw JSON response

## Notes

- Requires `PERPLEXITY_API_KEY` environment variable
- Responses include citations when available
- Batch queries are processed in a single API call

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
