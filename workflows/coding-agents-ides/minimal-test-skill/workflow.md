# minimal-test-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mig6671/minimal-test-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mig6671/minimal-test-skill/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Minimal test skill for debugging ClawHub publishing

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Minimal test skill for debugging ClawHub publishing

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run minimal-test-skill`)
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
You are executing the minimal-test-skill workflow. Use the following context:

Description: Minimal test skill for debugging ClawHub publishing

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: minimal-test-skill
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Minimal Test

This is a test skill.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
