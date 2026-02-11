# template-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/seanphan/template-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/seanphan/template-skill/SKILL.md)
> Category: AI & LLMs

---

## Description

Replace with description of the skill and when Claude should use it.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Replace with description of the skill and when Claude should use it.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run template-skill`)
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
You are executing the template-skill workflow. Use the following context:

Description: Replace with description of the skill and when Claude should use it.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: template-skill
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Insert instructions below

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
