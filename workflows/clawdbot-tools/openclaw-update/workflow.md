# openclaw-update

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/realowg/openclaw-update/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/realowg/openclaw-update/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Comprehensive backup, update, and restore workflow with dynamic workspace detection

**Homepage:** https://github.com/pasogott/openclaw-update-skill
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Comprehensive backup, update, and restore workflow with dynamic workspace detection

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run openclaw-update`)
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
You are executing the openclaw-update workflow. Use the following context:

Description: Comprehensive backup, update, and restore workflow with dynamic workspace detection

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openclaw-update
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: https://github.com/pasogott/openclaw-update-skill
```

---

## Original Skill Content



---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
