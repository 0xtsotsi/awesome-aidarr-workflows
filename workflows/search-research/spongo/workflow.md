# spongo

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/nabssku/spongo/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/nabssku/spongo/SKILL.md)
> Category: Search & Research

---

## Description

Terminal Spotify playback/search via spogo (preferred) or spotify_player.

**Homepage:** https://www.spotify.com
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Terminal Spotify playback/search via spogo (preferred) or spotify_player.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run spongo`)
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
You are executing the spongo workflow. Use the following context:

Description: Terminal Spotify playback/search via spogo (preferred) or spotify_player.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: spongo
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: https://www.spotify.com
```

---

## Original Skill Content



# spogo / spotify_player

Use `spogo` **(preferred)** for Spotify playback/search. Fall back to `spotify_player` if needed.

Requirements
- Spotify Premium account.
- Either `spogo` or `spotify_player` installed.

spogo setup
- Import cookies: `spogo auth import --browser chrome`

Common CLI commands
- Search: `spogo search track "query"`
- Playback: `spogo play|pause|next|prev`
- Devices: `spogo device list`, `spogo device set "<name|id>"`
- Status: `spogo status`

spotify_player commands (fallback)
- Search: `spotify_player search "query"`
- Playback: `spotify_player playback play|pause|next|previous`
- Connect device: `spotify_player connect`
- Like track: `spotify_player like`

Notes
- Config folder: `~/.config/spotify-player` (e.g., `app.toml`).
- For Spotify Connect integration, set a user `client_id` in config.
- TUI shortcuts are available via `?` in the app.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
