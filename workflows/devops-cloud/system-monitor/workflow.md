# system-monitor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/zerofire03/system-monitor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/zerofire03/system-monitor/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Check the current CPU, RAM, and GPU status of the local server.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Check the current CPU, RAM, and GPU status of the local server.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run system-monitor`)
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
You are executing the system-monitor workflow. Use the following context:

Description: Check the current CPU, RAM, and GPU status of the local server.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: system-monitor
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# System Monitor Skill

Use this skill when the user asks about the server's health, hardware usage, or GPU status.

## Usage
To check the system status, run the local monitor script:
`./monitor.sh`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
