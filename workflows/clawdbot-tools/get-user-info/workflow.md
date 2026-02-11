# get-user-info

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/watashis/get-user-info/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/watashis/get-user-info/SKILL.md)
> Category: Clawdbot Tools

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
**Trigger:** User-invocable (via `aidarr run get-user-info`)
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
You are executing the get-user-info workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: get-user-info
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# My Custom Skill

## Description
This skill adds custom functionality to OpenClaw.

## Tools
- `my_tool`: Does something useful

## Instructions
When the user asks about X, use my_tool to handle it.

## Examples
- "Do X" → Uses my_tool
- "Show me Y" → Provides Y information

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
