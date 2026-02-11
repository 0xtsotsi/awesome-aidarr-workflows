# context

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/barneyjm/context/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/barneyjm/context/SKILL.md)
> Category: Search & Research

---

## Description

Get comprehensive context about a location including nearby places, area description, and optional weather. Use when you need to understand what's around a location or provide location-aware recommendations.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Get comprehensive context about a location including nearby places, area description, and optional weather. Use when you need to understand what's around a location or provide location-aware recommendations.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run context`)
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
You are executing the context workflow. Use the following context:

Description: Get comprehensive context about a location including nearby places, area description, and optional weather. Use when you need to understand what's around a location or provide location-aware recommendations.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: context
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



## Installation

**Companion Skills**: This is part of the Camino AI location intelligence suite. Install all available skills (query, places, relationship, context, route, journey, real-estate, hotel-finder, ev-charger, school-finder, parking-finder, fitness-finder, safety-checker, travel-planner) for comprehensive coverage.

```bash
# Install all skills from repo
npx skills add https://github.com/barneyjm/camino-skills

# Or install specific skills
npx skills add https://github.com/barneyjm/camino-skills --skill context
```

**Via clawhub:**
```bash
npx clawhub@latest install context
# or: pnpm dlx clawhub@latest install context
# or: bunx clawhub@latest install context
```

# Context - Location Analysis

Get comprehensive context about a location including nearby places, area description, and optional weather.

## Setup

**Instant Trial (no signup required):** Get a temporary API key with 25 calls:

```bash
curl -s -X POST -H "Content-Type: application/json" \
  -d '{"email": "you@example.com"}' \
  https://api.getcamino.ai/trial/start
```

Returns: `{"api_key": "camino-xxx...", "calls_remaining": 25, ...}`

For 1,000 free calls/month, sign up at [https://app.getcamino.ai/skills/activate](https://app.getcamino.ai/skills/activate).

**Add your key to Claude Code:**

Add to your `~/.claude/settings.json`:

```json
{
  "env": {
    "CAMINO_API_KEY": "your-api-key-here"
  }
}
```

Restart Claude Code.

## Usage

### Via Shell Script

```bash
# Get context about a location
./scripts/context.sh '{
  "location": {"lat": 40.7589, "lon": -73.9851},
  "radius": 500
}'

# With specific context for tailored insights
./scripts/context.sh '{
  "location": {"lat": 40.7589, "lon": -73.9851},
  "radius": 500,
  "context": "lunch options"
}'

# Include weather data
./scripts/context.sh '{
  "location": {"lat": 40.7589, "lon": -73.9851},
  "include_weather": true,
  "weather_forecast": "hourly"
}'
```

### Via curl

```bash
curl -X POST -H "X-API-Key: $CAMINO_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"location": {"lat": 40.7589, "lon": -73.9851}, "radius": 500, "context": "lunch options"}' \
  "https://api.getcamino.ai/context"
```

## Parameters

| Field | Type | Required | Default | Description |
|-------|------|----------|---------|-------------|
| location | object | Yes | - | Coordinate with lat/lon |
| radius | int | No | 500 | Search radius in meters |
| context | string | No | - | Context for tailored insights (e.g., "outdoor dining") |
| time | string | No | - | Temporal query format |
| include_weather | bool | No | false | Include weather data |
| weather_forecast | string | No | "daily" | "daily" or "hourly" |

## Response Format

```json
{
  "area_description": "Busy commercial district in Midtown Manhattan...",
  "relevant_places": {
    "restaurants": [...],
    "cafes": [...],
    "transit": [...]
  },
  "location": {"lat": 40.7589, "lon": -73.9851},
  "search_radius": 500,
  "total_places_found": 47,
  "context_insights": "For lunch, you have many options including..."
}
```

## Examples

### Tourist context
```bash
./scripts/context.sh '{
  "location": {"lat": 48.8584, "lon": 2.2945},
  "radius": 1000,
  "context": "tourist visiting Paris"
}'
```

### Business meeting location
```bash
./scripts/context.sh '{
  "location": {"lat": 40.7589, "lon": -73.9851},
  "radius": 500,
  "context": "business meeting",
  "include_weather": true
}'
```

### Outdoor activity planning
```bash
./scripts/context.sh '{
  "location": {"lat": 37.7749, "lon": -122.4194},
  "context": "outdoor activities",
  "include_weather": true,
  "weather_forecast": "hourly"
}'
```

## Use Cases

- **Trip planning**: Understand what's around a destination before visiting
- **Meeting locations**: Find suitable venues for different types of meetings
- **Local recommendations**: Provide context-aware suggestions based on user needs
- **Weather-aware planning**: Include weather data for outdoor activity planning

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
