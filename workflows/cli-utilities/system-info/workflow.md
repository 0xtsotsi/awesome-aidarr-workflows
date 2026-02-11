# system-info

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xejrax/system-info/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xejrax/system-info/SKILL.md)
> Category: CLI Utilities

---

## Description

Quick system diagnostics: CPU, memory, disk, uptime

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Quick system diagnostics: CPU, memory, disk, uptime

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run system-info`)
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
You are executing the system-info workflow. Use the following context:

Description: Quick system diagnostics: CPU, memory, disk, uptime

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: system-info
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# System Info

Quick system diagnostics covering CPU, memory, disk, and uptime. Uses standard Linux utilities that are always available.

## Commands

```bash
# Show all system info (CPU, memory, disk, uptime)
system-info

# Show CPU information
system-info cpu

# Show memory usage
system-info mem

# Show disk usage
system-info disk

# Show system uptime
system-info uptime
```

## Install

No installation needed. `free` and related utilities are always present on the system.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
