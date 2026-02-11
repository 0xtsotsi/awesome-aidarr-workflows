# morning-briefing

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/lucas-riverbi/morning-briefing/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/lucas-riverbi/morning-briefing/SKILL.md)
> Category: Productivity & Tasks

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run morning-briefing`)
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
You are executing the morning-briefing workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: morning-briefing
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

---
name: morning-briefing
description: Generate personalized morning report with today's reminders, Notion tasks (undone), and vault storage. Use when user asks for morning briefing, daily summary, or &quot;today's plan&quot;. Pulls from Apple Reminders (as calendar proxy) and Notion tasks DB (set NOTION_TASKS_DB or specify DB ID).
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
