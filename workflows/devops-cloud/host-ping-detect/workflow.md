# host-ping-detect

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ray-778/host-ping-detect/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ray-778/host-ping-detect/SKILL.md)
> Category: DevOps & Cloud

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
**Trigger:** User-invocable (via `aidarr run host-ping-detect`)
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
You are executing the host-ping-detect workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: host-ping-detect
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



## Usage Instructions for the Agent

To use this skill, execute a ping command on the host IP 39.106.7.8. Use shell execution to run:

```bash
ping -c 4 39.106.7.8  # Send 4 ping packets (cross-platform compatible)
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
