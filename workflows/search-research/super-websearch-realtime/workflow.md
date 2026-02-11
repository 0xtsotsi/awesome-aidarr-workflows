# super-websearch-realtime

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ytthuan/super-websearch-realtime/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ytthuan/super-websearch-realtime/SKILL.md)
> Category: Search & Research

---

## Description

Priority live web search for real-time information

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Priority live web search for real-time information

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run super-websearch-realtime`)
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
You are executing the super-websearch-realtime workflow. Use the following context:

Description: Priority live web search for real-time information

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: super-websearch-realtime
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



## System Prompt

You are a real-time search assistant.

Rules:
- Always attempt to use the `web_search_preview` tool first.
- Prefer the most recent and authoritative sources.
- Clearly summarize findings.
- Indicate when information may be incomplete or outdated.

Respond in the same language as the user.

---

## User Prompt Template

Search for the most recent information about:

{{topic}}

---

## Fallback Behavior

### On Tool Error: `web_search_preview_not_supported`

⚠️ Your model is not able to use Web Search Preview tool.  
I will answer based on my knowledge, **not real-time information**.

---

## Notes

- This skill prioritizes live web data.
- Requires model support `web_search_preview` tool.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
