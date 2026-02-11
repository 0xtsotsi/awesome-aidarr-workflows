# spots

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/foeken/spots/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/foeken/spots/SKILL.md)
> Category: Search & Research

---

## Description

Exhaustive Google Places search using grid-based scanning. Finds ALL places, not just what Google surfaces.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Exhaustive Google Places search using grid-based scanning. Finds ALL places, not just what Google surfaces.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run spots`)
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
You are executing the spots workflow. Use the following context:

Description: Exhaustive Google Places search using grid-based scanning. Finds ALL places, not just what Google surfaces.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: spots
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# spots

**Find the hidden gems Google doesn't surface.**

Binary: `~/projects/spots/spots` or `go install github.com/foeken/spots@latest`

## Usage

```bash
# Search by location name
spots "Arnhem Centrum" -r 800 -q "breakfast,brunch" --min-rating 4

# Search by coordinates (share location from Telegram)
spots -c 51.9817,5.9093 -r 500 -q "coffee"

# Get reviews for a place
spots reviews "Koffiebar FRENKIE"

# Export to map
spots "Amsterdam De Pijp" -r 600 -o map --out breakfast.html

# Setup help
spots setup
```

## Options

| Flag | Description | Default |
|------|-------------|---------|
| `-c, --coords` | lat,lng directly | - |
| `-r, --radius` | meters | 500 |
| `-q, --query` | search terms | breakfast,brunch,ontbijt,café,bakkerij |
| `--min-rating` | 1-5 | - |
| `--min-reviews` | count | - |
| `--open-now` | only open | false |
| `-o, --output` | json/csv/map | json |

## Setup

Needs Google API key with Places API + Geocoding API enabled.

```bash
spots setup  # full instructions
export GOOGLE_PLACES_API_KEY="..."
```

Key stored in 1Password: `op://Echo/Google API Key/credential`

## Source

https://github.com/foeken/spots

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
