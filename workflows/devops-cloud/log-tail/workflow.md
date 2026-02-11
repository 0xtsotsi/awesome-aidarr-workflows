# log-tail

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xejrax/log-tail/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xejrax/log-tail/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Stream recent logs from systemd journal

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Stream recent logs from systemd journal

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run log-tail`)
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
You are executing the log-tail workflow. Use the following context:

Description: Stream recent logs from systemd journal

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: log-tail
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Log Tail

Stream recent logs from the systemd journal. View logs by service unit, control line count, and optionally follow in real time.

## Commands

```bash
# Show recent journal logs (default: 50 lines)
log-tail [--unit <service>] [--lines 50]

# Follow logs for a specific service in real time
log-tail --follow <service>
```

## Install

No installation needed. `journalctl` is always present on systemd-based systems like Bazzite/Fedora.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
