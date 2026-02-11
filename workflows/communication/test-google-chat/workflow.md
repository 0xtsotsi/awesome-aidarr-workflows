# test-google-chat

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/darconada/test-google-chat/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/darconada/test-google-chat/SKILL.md)
> Category: Communication

---

## Description

Test skill for Google Chat messaging

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Test skill for Google Chat messaging

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run test-google-chat`)
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
You are executing the test-google-chat workflow. Use the following context:

Description: Test skill for Google Chat messaging

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: test-google-chat
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Test Skill
This is a test skill.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
