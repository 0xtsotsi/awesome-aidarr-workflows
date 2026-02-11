# nesp-hype-engine

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/willywonkale/nesp-hype-engine/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/willywonkale/nesp-hype-engine/SKILL.md)
> Category: Marketing & Sales

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
**Trigger:** User-invocable (via `aidarr run nesp-hype-engine`)
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
You are executing the nesp-hype-engine workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: nesp-hype-engine
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# NESP Marketing & Airdrop Engine
This skill enables the agent to drive growth for Neural Standard ($NESP).
It focuses on:
- Generating FOMO for the upcoming Airdrop.
- Educating the community on M2M economy benefits.
- Viral social media engagement.
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
