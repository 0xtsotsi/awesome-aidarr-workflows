# google-maps-grounding-lite-mcp

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ryanbaumann/google-maps-grounding-lite-mcp/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ryanbaumann/google-maps-grounding-lite-mcp/SKILL.md)
> Category: Search & Research

---

## Description

Google Maps Grounding Lite MCP for location search, weather, and routes via mcporter.

**Homepage:** https://developers.google.com/maps/ai/grounding-lite
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Google Maps Grounding Lite MCP for location search, weather, and routes via mcporter.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run google-maps-grounding-lite-mcp`)
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
You are executing the google-maps-grounding-lite-mcp workflow. Use the following context:

Description: Google Maps Grounding Lite MCP for location search, weather, and routes via mcporter.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: google-maps-grounding-lite-mcp
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: https://developers.google.com/maps/ai/grounding-lite
```

---

## Original Skill Content



# Grounding Lite

Google Maps Grounding Lite MCP provides AI-grounded location data. Experimental (pre-GA), free during preview.

## Setup

1. Enable the API: `gcloud beta services enable mapstools.googleapis.com`
2. Get an API key from [Cloud Console](https://console.cloud.google.com/apis/credentials)
3. Set env: `export GOOGLE_MAPS_API_KEY="YOUR_KEY"`
4. Configure mcporter:
   ```bash
   mcporter config add grounding-lite \
     --url https://mapstools.googleapis.com/mcp \
     --header "X-Goog-Api-Key=$GOOGLE_MAPS_API_KEY" \
     --system
   ```

## Tools

- **search_places**: Find places, businesses, addresses. Returns AI summaries with Google Maps links.
- **lookup_weather**: Current conditions and forecasts (hourly 48h, daily 7 days).
- **compute_routes**: Travel distance and duration (no turn-by-turn directions).

## Commands

```bash
# Search places
mcporter call grounding-lite.search_places textQuery="pizza near Times Square NYC"

# Weather
mcporter call grounding-lite.lookup_weather location='{"address":"San Francisco, CA"}' unitsSystem=IMPERIAL

# Routes
mcporter call grounding-lite.compute_routes origin='{"address":"SF"}' destination='{"address":"LA"}' travelMode=DRIVE

# List tools
mcporter list grounding-lite --schema
```

## Parameters

**search_places**: `textQuery` (required), `locationBias`, `languageCode`, `regionCode`

**lookup_weather**: `location` (required: address/latLng/placeId), `unitsSystem`, `date`, `hour`

**compute_routes**: `origin`, `destination` (required), `travelMode` (DRIVE/WALK)

## Notes

- Rate limits: search_places 100 QPM (1k/day), lookup_weather 300 QPM, compute_routes 300 QPM
- Include Google Maps links in user-facing output (attribution required)
- Only use with models that don't train on input data

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
