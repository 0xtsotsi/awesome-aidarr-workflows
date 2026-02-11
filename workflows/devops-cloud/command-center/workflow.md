# command-center

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jontsai/command-center/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jontsai/command-center/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Mission control dashboard for OpenClaw - real-time session monitoring, LLM usage tracking, cost intelligence, and system vitals. View all your AI agents in one place.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.1

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Mission control dashboard for OpenClaw - real-time session monitoring, LLM usage tracking, cost intelligence, and system vitals. View all your AI agents in one place.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run command-center`)
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
You are executing the command-center workflow. Use the following context:

Description: Mission control dashboard for OpenClaw - real-time session monitoring, LLM usage tracking, cost intelligence, and system vitals. View all your AI agents in one place.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: command-center
category: DevOps & Cloud
version: 1.0.1
user_invocable: True
homepage: 
```

---

## Original Skill Content



# OpenClaw Command Center

Mission control for your AI workforce.

## Quick Start

```bash
# Install from ClawHub
clawhub install command-center

# Start the dashboard
cd ~/.openclaw/skills/command-center
node lib/server.js
```

Dashboard runs at **http://localhost:3333**

## Features

- **Session Monitoring** — Real-time view of all AI sessions with live updates
- **LLM Fuel Gauges** — Track Claude, Codex, and other model usage
- **System Vitals** — CPU, Memory, Disk, Temperature
- **Cron Jobs** — View and manage scheduled tasks
- **Cerebro Topics** — Automatic conversation organization
- **Cost Tracking** — Per-session costs, projections, savings estimates
- **Privacy Controls** — Hide sensitive topics for demos

## Configuration

The dashboard auto-detects your OpenClaw workspace. Set `OPENCLAW_WORKSPACE` to override.

### Authentication

| Mode | Use Case |
|------|----------|
| `none` | Local development |
| `token` | Remote access |
| `tailscale` | Team VPN |
| `cloudflare` | Public deployment |

```bash
DASHBOARD_AUTH_MODE=tailscale node lib/server.js
```

## API

| Endpoint | Description |
|----------|-------------|
| `GET /api/state` | All dashboard data (unified) |
| `GET /api/events` | SSE stream for live updates |
| `GET /api/health` | Health check |

## Links

- [GitHub](https://github.com/jontsai/openclaw-command-center)
- [Documentation](https://github.com/jontsai/openclaw-command-center#readme)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
