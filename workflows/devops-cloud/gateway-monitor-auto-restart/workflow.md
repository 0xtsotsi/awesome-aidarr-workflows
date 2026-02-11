# gateway-monitor-auto-restart

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/shirley6692026/gateway-monitor-auto-restart/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/shirley6692026/gateway-monitor-auto-restart/SKILL.md)
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
**Trigger:** User-invocable (via `aidarr run gateway-monitor-auto-restart`)
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
You are executing the gateway-monitor-auto-restart workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: gateway-monitor-auto-restart
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Gateway Monitor Auto-Restart Skill

Automatically monitors the OpenClaw gateway status and restarts it if it becomes unresponsive. Features 3-hour checks, smart restart logic, issue diagnosis, and 7-day log rotation.

## Description

This skill provides comprehensive monitoring for the OpenClaw gateway with automatic restart capabilities. It includes:

- Health checks every 3 hours
- Smart restart mechanism when gateway is down
- Issue diagnosis when startup fails
- 7-day log rotation system
- Fast recovery system that prioritizes quick gateway restart

## Features

- **Automatic Monitoring**: Checks gateway status every 3 hours
- **Smart Restart**: Restarts gateway when it becomes unresponsive
- **Issue Diagnosis**: Identifies and reports startup issues
- **Fast Recovery**: Prioritizes quick gateway restart
- **Log Management**: Maintains logs with 7-day rotation
- **Error Handling**: Gracefully handles "already running" errors

## Usage

The skill automatically sets up a cron job that runs the monitoring script every 3 hours. The monitoring system will:

1. Check if the gateway is responsive
2. If unresponsive, attempt to restart it
3. If restart fails, diagnose the issue
4. Log all activities with timestamp
5. Rotate logs older than 7 days

## Requirements

- OpenClaw gateway installed and configured
- Proper permissions to manage gateway service
- Cron access for scheduling checks

## Configuration

No additional configuration required. The skill automatically installs the monitoring system with optimal settings.
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
