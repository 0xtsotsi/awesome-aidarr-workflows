# surfline

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/miguelcarranza/surfline/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/miguelcarranza/surfline/SKILL.md)
> Category: Transportation

---

## Description

Get surf forecasts and current conditions from Surfline public endpoints (no login). Use to look up Surfline spot IDs, fetch forecasts/conditions for specific spots, and summarize multiple favorite spots.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Get surf forecasts and current conditions from Surfline public endpoints (no login). Use to look up Surfline spot IDs, fetch forecasts/conditions for specific spots, and summarize multiple favorite spots.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run surfline`)
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
You are executing the surfline workflow. Use the following context:

Description: Get surf forecasts and current conditions from Surfline public endpoints (no login). Use to look up Surfline spot IDs, fetch forecasts/conditions for specific spots, and summarize multiple favorite spots.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: surfline
category: Transportation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Surfline (public, no login)

This skill uses Surfline **public endpoints** (no account, no cookies).

## Quick start

1) Find a spot id:

```bash
python3 scripts/surfline_search.py "Cardiff Reef"
python3 scripts/surfline_search.py "D Street"
```

2) Get a report for a spot id (prints text + JSON by default):

```bash
python3 scripts/surfline_report.py <spotId>
# or only one format:
python3 scripts/surfline_report.py <spotId> --text
python3 scripts/surfline_report.py <spotId> --json
```

3) Favorites summary (multiple spots) (prints text + JSON by default):

Create `~/.config/surfline/favorites.json` (see `references/favorites.json.example`).

```bash
python3 scripts/surfline_favorites.py
```

## Notes

- Keep requests gentle: don’t hammer endpoints. Scripts include basic caching.
- Spot IDs are stable; store them once.
- If Surfline changes endpoints/fields, update `scripts/surfline_client.py`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
