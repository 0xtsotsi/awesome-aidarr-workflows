# ultrahuman-openclaw

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/devpranoy/ultrahuman-openclaw/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/devpranoy/ultrahuman-openclaw/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Fetch and summarize Ultrahuman Ring/CGM metrics inside OpenClaw using the Ultrahuman MCP server (via mcporter). Use when the user asks about Ultrahuman data such as sleep score, total sleep, sleep stages, HR/HRV/RHR, steps, recovery index, movement index, VO2 max, or wants a daily/weekly Ultrahuman summary.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Fetch and summarize Ultrahuman Ring/CGM metrics inside OpenClaw using the Ultrahuman MCP server (via mcporter). Use when the user asks about Ultrahuman data such as sleep score, total sleep, sleep stages, HR/HRV/RHR, steps, recovery index, movement index, VO2 max, or wants a daily/weekly Ultrahuman summary.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run ultrahuman-openclaw`)
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
You are executing the ultrahuman-openclaw workflow. Use the following context:

Description: Fetch and summarize Ultrahuman Ring/CGM metrics inside OpenClaw using the Ultrahuman MCP server (via mcporter). Use when the user asks about Ultrahuman data such as sleep score, total sleep, sleep stages, HR/HRV/RHR, steps, recovery index, movement index, VO2 max, or wants a daily/weekly Ultrahuman summary.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ultrahuman-openclaw
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Ultrahuman (OpenClaw)

Fetch Ultrahuman metrics via **Ultrahuman MCP** and **mcporter**, then summarize them.

## Setup (one-time)

You need:

1) **Ultrahuman Developer/Partner credentials**

You need a personal auth token from Ultrahuman Developer Portal:
- https://vision.ultrahuman.com/developer

Then set:
- `ULTRAHUMAN_USER_EMAIL`
- `ULTRAHUMAN_AUTH_TOKEN` (your personal token)
- (Also set your Partner ID in the Ultrahuman app, if provided/required)

2) **Ultrahuman MCP server**

Repository:
- https://github.com/Monasterolo21/Ultrahuman-MCP

Build it (example):
- `bun install && bun run build`
- You should end up with an entrypoint like: `dist/main.js`

3) **mcporter config** that defines an MCP server named `ultrahuman`

Example `config/mcporter.json` (adjust path to your built `main.js`):

```json
{
  "mcpServers": {
    "ultrahuman": {
      "transport": "stdio",
      "command": "node",
      "args": ["/absolute/path/to/Ultrahuman-MCP/dist/main.js"],
      "env": {
        "ULTRAHUMAN_AUTH_TOKEN": "${ULTRAHUMAN_AUTH_TOKEN}",
        "ULTRAHUMAN_USER_EMAIL": "${ULTRAHUMAN_USER_EMAIL}"
      }
    }
  }
}
```

## Quick start

### Daily summary (recommended)

From your OpenClaw workspace (so `./config/mcporter.json` is found):

```bash
cd /path/to/your/openclaw/workspace
python3 skills/local/ultrahuman-openclaw/scripts/ultrahuman_summary.py --yesterday
```

Specific date:

```bash
python3 skills/local/ultrahuman-openclaw/scripts/ultrahuman_summary.py --date YYYY-MM-DD
```

If your mcporter config isn’t at `./config/mcporter.json`, pass it explicitly:

```bash
python3 skills/local/ultrahuman-openclaw/scripts/ultrahuman_summary.py \
  --date YYYY-MM-DD \
  --mcporter-config /path/to/mcporter.json
```

### Raw JSON

```bash
mcporter --config /path/to/mcporter.json \
  call ultrahuman.ultrahuman_metrics date=YYYY-MM-DD --output json
```

## What to report (default)

Keep summaries short unless asked:

- Sleep score + total sleep + efficiency + restorative sleep + deep/REM
- Steps total
- Recovery index, movement index, active minutes
- VO2 max, sleep HRV, RHR

If sleep score/total sleep are in a "Needs attention" state, call it out explicitly.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
