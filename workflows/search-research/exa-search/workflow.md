# exa-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xinhai-ai/exa-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xinhai-ai/exa-search/SKILL.md)
> Category: Search & Research

---

## Description

Use Exa (exa.ai) Search API to search the web and return structured results (title/url/snippet/text) via a local Node script. Trigger when the user asks to enable Exa search, configure Exa API key, or perform web search using Exa.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Use Exa (exa.ai) Search API to search the web and return structured results (title/url/snippet/text) via a local Node script. Trigger when the user asks to enable Exa search, configure Exa API key, or perform web search using Exa.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run exa-search`)
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
You are executing the exa-search workflow. Use the following context:

Description: Use Exa (exa.ai) Search API to search the web and return structured results (title/url/snippet/text) via a local Node script. Trigger when the user asks to enable Exa search, configure Exa API key, or perform web search using Exa.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: exa-search
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Exa Search

Use Exa’s Search API via the bundled script.

## Requirements

- Set `EXA_API_KEY` in the Gateway environment (recommended) or in `~/.openclaw/.env`.

## Commands

- Run a search:
  - `node {baseDir}/scripts/exa_search.mjs "<query>" --count 5`

- Include page text in results (costs more):
  - `node {baseDir}/scripts/exa_search.mjs "<query>" --count 5 --text`

- Narrow by time window:
  - `--start 2025-01-01 --end 2026-02-04`

## Notes

- This skill does not modify `web_search`; it provides an Exa-backed alternative you can invoke when you specifically want Exa.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
