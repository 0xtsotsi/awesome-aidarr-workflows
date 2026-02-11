# uptime-kuma

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/msarheed/uptime-kuma/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/msarheed/uptime-kuma/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Interact with Uptime Kuma monitoring server. Use for checking monitor status, adding/removing monitors, pausing/resuming checks, viewing heartbeat history. Triggers on mentions of Uptime Kuma, server monitoring, uptime checks, or service health monitoring.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Interact with Uptime Kuma monitoring server. Use for checking monitor status, adding/removing monitors, pausing/resuming checks, viewing heartbeat history. Triggers on mentions of Uptime Kuma, server monitoring, uptime checks, or service health monitoring.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run uptime-kuma`)
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
You are executing the uptime-kuma workflow. Use the following context:

Description: Interact with Uptime Kuma monitoring server. Use for checking monitor status, adding/removing monitors, pausing/resuming checks, viewing heartbeat history. Triggers on mentions of Uptime Kuma, server monitoring, uptime checks, or service health monitoring.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: uptime-kuma
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Uptime Kuma Skill

Manage Uptime Kuma monitors via CLI wrapper around the Socket.IO API.

## Setup

Requires `uptime-kuma-api` Python package:
```bash
pip install uptime-kuma-api
```

Environment variables (set in shell or Clawdbot config):
- `UPTIME_KUMA_URL` - Server URL (e.g., `http://localhost:3001`)
- `UPTIME_KUMA_USERNAME` - Login username
- `UPTIME_KUMA_PASSWORD` - Login password

## Usage

Script location: `scripts/kuma.py`

### Commands

```bash
# Overall status summary
python scripts/kuma.py status

# List all monitors
python scripts/kuma.py list
python scripts/kuma.py list --json

# Get monitor details
python scripts/kuma.py get <id>

# Add monitors
python scripts/kuma.py add --name "My Site" --type http --url https://example.com
python scripts/kuma.py add --name "Server Ping" --type ping --hostname 192.168.1.1
python scripts/kuma.py add --name "SSH Port" --type port --hostname server.local --port 22

# Pause/resume monitors
python scripts/kuma.py pause <id>
python scripts/kuma.py resume <id>

# Delete monitor
python scripts/kuma.py delete <id>

# View heartbeat history
python scripts/kuma.py heartbeats <id> --hours 24

# List notification channels
python scripts/kuma.py notifications
```

### Monitor Types

- `http` - HTTP/HTTPS endpoint
- `ping` - ICMP ping
- `port` - TCP port check
- `keyword` - HTTP + keyword search
- `dns` - DNS resolution
- `docker` - Docker container
- `push` - Push-based (passive)
- `mysql`, `postgres`, `mongodb`, `redis` - Database checks
- `mqtt` - MQTT broker
- `group` - Monitor group

### Common Workflows

**Check what's down:**
```bash
python scripts/kuma.py status
python scripts/kuma.py list  # Look for 🔴
```

**Add HTTP monitor with 30s interval:**
```bash
python scripts/kuma.py add --name "API Health" --type http --url https://api.example.com/health --interval 30
```

**Maintenance mode (pause all):**
```bash
for id in $(python scripts/kuma.py list --json | jq -r '.[].id'); do
  python scripts/kuma.py pause $id
done
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
