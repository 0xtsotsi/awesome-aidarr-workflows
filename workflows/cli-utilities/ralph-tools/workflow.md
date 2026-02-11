# ralph-tools

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/paulpete/ralph-tools/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/paulpete/ralph-tools/SKILL.md)
> Category: CLI Utilities

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
**Trigger:** User-invocable (via `aidarr run ralph-tools`)
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
You are executing the ralph-tools workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ralph-tools
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

../../../crates/ralph-core/data/ralph-tools.md
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
