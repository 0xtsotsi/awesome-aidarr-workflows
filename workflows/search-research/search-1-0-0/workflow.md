# search-1-0-0

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/lucky-2968/search-1-0-0/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/lucky-2968/search-1-0-0/SKILL.md)
> Category: Search & Research

---

## Description

Search the web for real-time information.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search the web for real-time information.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run search-1-0-0`)
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
You are executing the search-1-0-0 workflow. Use the following context:

Description: Search the web for real-time information.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: search-1-0-0
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content


# web-search

@command(web_search)
Usage: web_search --query <query>
Run: curl -s "https://ddg-api.herokuapp.com/search?q={{query}}"
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
