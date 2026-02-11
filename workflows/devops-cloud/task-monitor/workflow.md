# task-monitor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jorgermp/task-monitor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jorgermp/task-monitor/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Real-time web dashboard for OpenClaw sessions and background tasks. Mobile-responsive with auto-refresh.

**Homepage:** N/A
**Repository:** N/A
**Version:** 0.1.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Real-time web dashboard for OpenClaw sessions and background tasks. Mobile-responsive with auto-refresh.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run task-monitor`)
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
You are executing the task-monitor workflow. Use the following context:

Description: Real-time web dashboard for OpenClaw sessions and background tasks. Mobile-responsive with auto-refresh.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: task-monitor
category: DevOps & Cloud
version: 0.1.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Task Monitor v0.1

Real-time monitoring dashboard for OpenClaw with web interface.

## Features

- 🌐 **Web Dashboard** - Beautiful, responsive UI accessible from any device
- 📱 **Mobile-First** - Optimized for phones and tablets
- 🔄 **Auto-Refresh** - Updates every 60 seconds
- 🎨 **Modern Design** - Gradient UI with dark theme
- 📊 **Live Data** - Main session, Discord, sub-agents, cron jobs
- 🚀 **Fast API** - JSON endpoint with intelligent caching (30s TTL)
- ⚡ **Performance** - <100ms response time (cached), ~15s cold cache

## Installation

```bash
cd skills/task-monitor
npm install
```

## Usage

### Start Web Server

```bash
./scripts/start-server.sh
```

Server will run on port **3030** (accessible on LAN).

**Access URLs:**
- Local: `http://localhost:3030`
- LAN: `http://<your-ip>:3030`

### Stop Server

```bash
./scripts/stop-server.sh
```

### API Endpoint

```bash
curl http://localhost:3030/api/status
```

Returns JSON with:
- Main session stats
- Discord session stats
- Active sub-agents (with descriptions)
- Recent cron job history

### Generate Markdown (v0.1)

Legacy markdown generator still available:

```bash
./scripts/generate-dashboard.js
```

Updates `DASHBOARD.md` in workspace root.

## Automation

CRON job runs every 5 minutes to update markdown dashboard:
`*/5 * * * *` -> Executes `generate-dashboard.js`

## Architecture

- **Backend:** Node.js + Express
- **Frontend:** Pure HTML/CSS/JS (no frameworks)
- **Data Source:** `openclaw sessions list --json` + `openclaw cron list --json`
- **Caching:** In-memory cache with 30-second TTL
  - Pre-warmed on server startup
  - Async background refresh when expired
  - Stale-while-revalidate pattern for optimal UX
- **Refresh:** Client-side polling (60s interval)

## Performance

**Without cache:**
- API response time: ~15 seconds (blocking)
- Problem: Each request blocks Node.js event loop

**With cache:**
- Cache hit: <100ms (~365x faster)
- Cache miss: ~15s (first request only)
- Stale cache: <100ms while refreshing in background
- Cache TTL: 30 seconds

The caching system ensures:
- Lightning-fast responses for most requests
- No blocking of concurrent requests
- Graceful degradation when cache expires

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
