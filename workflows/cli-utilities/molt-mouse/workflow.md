# molt-mouse

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/oguzhaslak/molt-mouse/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/oguzhaslak/molt-mouse/SKILL.md)
> Category: CLI Utilities

---

## Description

Local mouse control via ydotool wrapper

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Local mouse control via ydotool wrapper

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run molt-mouse`)
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
You are executing the molt-mouse workflow. Use the following context:

Description: Local mouse control via ydotool wrapper

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: molt-mouse
category: CLI Utilities
version: 1.0.0
user_invocable: False
homepage: 
```

---

## Original Skill Content


When the user asks to move/click the mouse:
- Use the exec tool with host=gateway.
- ONLY run commands that start with: `molt-mouse ...`
- Supported:
  - `molt-mouse move <dx> <dy>`
  - `molt-mouse abs <x> <y>`
  - `molt-mouse click left|right|middle`
  - `molt-mouse click 0x40` # left button down (hold)
  - `molt-mouse click 0x80` # left button up (release)
- If numbers are missing/ambiguous, ask the user.


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
