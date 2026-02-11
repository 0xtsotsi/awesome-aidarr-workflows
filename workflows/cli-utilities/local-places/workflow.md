# local-places

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/local-places/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/local-places/SKILL.md)
> Category: CLI Utilities

---

## Description

Search for places (restaurants, cafes, etc.) via Google Places API proxy on localhost.

**Homepage:** https://github.com/Hyaxia/local_places
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search for places (restaurants, cafes, etc.) via Google Places API proxy on localhost.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run local-places`)
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
You are executing the local-places workflow. Use the following context:

Description: Search for places (restaurants, cafes, etc.) via Google Places API proxy on localhost.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: local-places
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: https://github.com/Hyaxia/local_places
```

---

## Original Skill Content



# 📍 Local Places

*Find places, Go fast*

Search for nearby places using a local Google Places API proxy. Two-step flow: resolve location first, then search.

## Setup

```bash
cd {baseDir}
echo "GOOGLE_PLACES_API_KEY=your-key" > .env
uv venv && uv pip install -e ".[dev]"
uv run --env-file .env uvicorn local_places.main:app --host 127.0.0.1 --port 8000
```

Requires `GOOGLE_PLACES_API_KEY` in `.env` or environment.

## Quick Start

1. **Check server:** `curl http://127.0.0.1:8000/ping`

2. **Resolve location:**
```bash
curl -X POST http://127.0.0.1:8000/locations/resolve \
  -H "Content-Type: application/json" \
  -d '{"location_text": "Soho, London", "limit": 5}'
```

3. **Search places:**
```bash
curl -X POST http://127.0.0.1:8000/places/search \
  -H "Content-Type: application/json" \
  -d '{
    "query": "coffee shop",
    "location_bias": {"lat": 51.5137, "lng": -0.1366, "radius_m": 1000},
    "filters": {"open_now": true, "min_rating": 4.0},
    "limit": 10
  }'
```

4. **Get details:**
```bash
curl http://127.0.0.1:8000/places/{place_id}
```

## Conversation Flow

1. If user says "near me" or gives vague location → resolve it first
2. If multiple results → show numbered list, ask user to pick
3. Ask for preferences: type, open now, rating, price level
4. Search with `location_bias` from chosen location
5. Present results with name, rating, address, open status
6. Offer to fetch details or refine search

## Filter Constraints

- `filters.types`: exactly ONE type (e.g., "restaurant", "cafe", "gym")
- `filters.price_levels`: integers 0-4 (0=free, 4=very expensive)
- `filters.min_rating`: 0-5 in 0.5 increments
- `filters.open_now`: boolean
- `limit`: 1-20 for search, 1-10 for resolve
- `location_bias.radius_m`: must be > 0

## Response Format

```json
{
  "results": [
    {
      "place_id": "ChIJ...",
      "name": "Coffee Shop",
      "address": "123 Main St",
      "location": {"lat": 51.5, "lng": -0.1},
      "rating": 4.6,
      "price_level": 2,
      "types": ["cafe", "food"],
      "open_now": true
    }
  ],
  "next_page_token": "..." 
}
```

Use `next_page_token` as `page_token` in next request for more results.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
