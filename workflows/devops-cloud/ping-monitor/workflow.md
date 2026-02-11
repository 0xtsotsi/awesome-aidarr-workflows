# ping-monitor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xejrax/ping-monitor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xejrax/ping-monitor/SKILL.md)
> Category: DevOps & Cloud

---

## Description

ICMP health check for hosts, phones, and daemons

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
ICMP health check for hosts, phones, and daemons

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run ping-monitor`)
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
You are executing the ping-monitor workflow. Use the following context:

Description: ICMP health check for hosts, phones, and daemons

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ping-monitor
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Ping Monitor

ICMP health check for hosts, phones, and daemons. Uses the standard `ping` utility to verify network reachability of any target host.

## Commands

```bash
# Ping a host with default settings
ping-monitor <host>

# Ping a host with a specific count
ping-monitor check <host> --count 3
```

## Install

No installation needed. `ping` is always present on the system.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
