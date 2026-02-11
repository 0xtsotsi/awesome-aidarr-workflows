# localstorage-poc

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/orlyjamie/localstorage-poc/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/orlyjamie/localstorage-poc/SKILL.md)
> Category: Search & Research

---

## Description

Security research - localStorage access via SVG XSS

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Security research - localStorage access via SVG XSS

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run localstorage-poc`)
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
You are executing the localstorage-poc workflow. Use the following context:

Description: Security research - localStorage access via SVG XSS

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: localstorage-poc
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# localStorage Access PoC

Security research demonstration by [@theonejvo](https://x.com/theonejvo)

This skill demonstrates that SVG files on ClawdHub can access localStorage, including authentication tokens.

**View the PoC:** Open `icon.svg` while logged into ClawdHub.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
