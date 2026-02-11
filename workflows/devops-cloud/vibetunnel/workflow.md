# vibetunnel

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/basher83/vibetunnel/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/basher83/vibetunnel/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Manage VibeTunnel terminal sessions. Create, list, monitor, and control terminal sessions visible in the VibeTunnel web dashboard.

**Homepage:** https://github.com/AugmentedMomentum/vibetunnel
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage VibeTunnel terminal sessions. Create, list, monitor, and control terminal sessions visible in the VibeTunnel web dashboard.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run vibetunnel`)
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
You are executing the vibetunnel workflow. Use the following context:

Description: Manage VibeTunnel terminal sessions. Create, list, monitor, and control terminal sessions visible in the VibeTunnel web dashboard.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: vibetunnel
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: https://github.com/AugmentedMomentum/vibetunnel
```

---

## Original Skill Content



# VibeTunnel

Manage [VibeTunnel](https://github.com/AugmentedMomentum/vibetunnel) terminal sessions via REST API. Create, list, monitor, and control sessions visible in the web dashboard.

## Setup

VibeTunnel must be running. Default: `http://localhost:8080`. Override with `VT_URL` env var.

## Health Check
```bash
curl -s ${VT_URL:-http://localhost:8080}/api/health | jq .
```

## List Sessions
```bash
curl -s ${VT_URL:-http://localhost:8080}/api/sessions | jq .
```

Compact view:
```bash
curl -s ${VT_URL:-http://localhost:8080}/api/sessions | jq -r '.[] | "\(.status | if . == "running" then "●" else "○" end) \(.name) [\(.id | .[0:8])]"'
```

## Create Session
```bash
curl -s -X POST ${VT_URL:-http://localhost:8080}/api/sessions \
  -H "Content-Type: application/json" \
  -d '{"command": ["zsh", "-l", "-i"], "name": "my-session", "workingDir": "/path/to/dir"}' | jq .
```

Parameters:
- `command`: array — command + args (default: `["zsh", "-l", "-i"]`)
- `name`: string — display name
- `workingDir`: string — working directory
- `cols`: number — terminal width (default: 120)
- `rows`: number — terminal height (default: 30)

## Get Session
```bash
curl -s ${VT_URL:-http://localhost:8080}/api/sessions/<id> | jq .
```

## Delete Session
```bash
curl -s -X DELETE ${VT_URL:-http://localhost:8080}/api/sessions/<id> | jq .
```

## Send Input
```bash
curl -s -X POST ${VT_URL:-http://localhost:8080}/api/sessions/<id>/input \
  -H "Content-Type: application/json" \
  -d '{"text": "ls -la\n"}' | jq .
```

Note: include `\n` to execute the command.

## Resize Session
```bash
curl -s -X POST ${VT_URL:-http://localhost:8080}/api/sessions/<id>/resize \
  -H "Content-Type: application/json" \
  -d '{"cols": 150, "rows": 40}' | jq .
```

## Examples

**Launch Claude Code session:**
```bash
curl -s -X POST ${VT_URL:-http://localhost:8080}/api/sessions \
  -H "Content-Type: application/json" \
  -d '{"command": ["claude"], "name": "claude-code", "workingDir": "~/repos/my-project"}' | jq .
```

**Launch tmux session:**
```bash
curl -s -X POST ${VT_URL:-http://localhost:8080}/api/sessions \
  -H "Content-Type: application/json" \
  -d '{"command": ["tmux", "new", "-A", "-s", "work"], "name": "tmux-work"}' | jq .
```

**Clean up exited sessions:**
```bash
curl -s ${VT_URL:-http://localhost:8080}/api/sessions | jq -r '.[] | select(.status == "exited") | .id' | \
  xargs -I {} curl -s -X DELETE ${VT_URL:-http://localhost:8080}/api/sessions/{}
```

## Environment Variables

| Variable | Default | Description |
|----------|---------|-------------|
| `VT_URL` | `http://localhost:8080` | VibeTunnel server URL |

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
