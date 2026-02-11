# opensysinfo-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/pr1vateer/opensysinfo-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/pr1vateer/opensysinfo-skill/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Small skill that reports basic system information (OS, uptime, CPU, memory, disk). Implemented in Bash.

**Homepage:** N/A
**Repository:** N/A
**Version:** 0.1.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Small skill that reports basic system information (OS, uptime, CPU, memory, disk). Implemented in Bash.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run opensysinfo-skill`)
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
You are executing the opensysinfo-skill workflow. Use the following context:

Description: Small skill that reports basic system information (OS, uptime, CPU, memory, disk). Implemented in Bash.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: opensysinfo-skill
category: Web & Frontend Development
version: 0.1.0
user_invocable: True
homepage: 
```

---

## Original Skill Content


# sysinfo-skill

A tiny OpenClaw skill that reports host system information. The implementation is pure Bash and requires `bash` to run.

Entrypoint: `{baseDir}/scripts/sysinfo.sh`
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
