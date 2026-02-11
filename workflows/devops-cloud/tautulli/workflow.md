# tautulli

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/rjmurillo/tautulli/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/rjmurillo/tautulli/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Monitor Plex activity and stats via Tautulli API. Check who's watching, view history, get library stats, and see server info.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Monitor Plex activity and stats via Tautulli API. Check who's watching, view history, get library stats, and see server info.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tautulli`)
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
You are executing the tautulli workflow. Use the following context:

Description: Monitor Plex activity and stats via Tautulli API. Check who's watching, view history, get library stats, and see server info.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tautulli
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Tautulli

Monitor Plex Media Server activity via Tautulli API.

## Setup

Set environment variables:
- `TAUTULLI_URL` – Tautulli instance URL (e.g., `http://192.168.1.100:8181`)
- `TAUTULLI_API_KEY` – Settings → Web Interface → API Key

## Commands

### Current Activity

```bash
bash {baseDir}/scripts/activity.sh
```

Shows active streams with user, title, progress, quality, and player.

### Watch History

```bash
bash {baseDir}/scripts/history.sh [limit]
```

Default: last 10 items. Pass a number for more.

### Library Stats

```bash
bash {baseDir}/scripts/libraries.sh
```

Lists library sections with item counts.

### Recently Added

```bash
bash {baseDir}/scripts/recent.sh [limit]
```

Shows recently added media. Default: 10 items.

### User Stats

```bash
bash {baseDir}/scripts/users.sh
```

Lists users with total watch time and last seen date.

### Server Info

```bash
bash {baseDir}/scripts/server.sh
```

Shows Plex server name, version, platform, and connection status.

## API Reference

All Tautulli API calls use:

```
$TAUTULLI_URL/api/v2?apikey=$TAUTULLI_API_KEY&cmd=<command>
```

Common commands: `get_activity`, `get_history`, `get_libraries`, `get_recently_added`, `get_users`, `get_server_info`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
