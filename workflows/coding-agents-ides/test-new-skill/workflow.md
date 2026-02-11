# test-new-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/tianshizhimao-sudo/test-new-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/tianshizhimao-sudo/test-new-skill/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Test skill for debugging

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Test skill for debugging

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run test-new-skill`)
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
You are executing the test-new-skill workflow. Use the following context:

Description: Test skill for debugging

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: test-new-skill
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Test Skill

This is a test.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
