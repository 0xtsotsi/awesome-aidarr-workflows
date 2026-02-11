# weather-pollen

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/thesethrose/weather-pollen/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/thesethrose/weather-pollen/SKILL.md)
> Category: Smart Home & IoT

---

## Description

Weather and pollen reports for any location using free APIs. Get current conditions, forecasts, and pollen data.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Weather and pollen reports for any location using free APIs. Get current conditions, forecasts, and pollen data.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run weather-pollen`)
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
You are executing the weather-pollen workflow. Use the following context:

Description: Weather and pollen reports for any location using free APIs. Get current conditions, forecasts, and pollen data.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: weather-pollen
category: Smart Home & IoT
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Weather and Pollen Skill

Get weather and pollen reports for any location using free APIs.

## Usage

When asked about weather or pollen in Anna, TX (or configured location), use the `weather_report` tool from this skill.

## Tools

### weather_report
Get weather and pollen data for a specified location.

**Args:**
- `includePollen` (boolean, default: true) - Include pollen data
- `location` (string, optional) - Location name to display (coordinates configured via env)

**Example:**
```json
{"includePollen": true, "location": "Anna, TX"}
```

## Configuration

Set location via environment variables (defaults for Anna, TX):
- `WEATHER_LAT` - Latitude (default: 33.3506)
- `WEATHER_LON` - Longitude (default: -96.3175)
- `WEATHER_LOCATION` - Location display name (default: "Anna, TX")

## APIs Used
- **Weather:** Open-Meteo (free, no API key)
- **Pollen:** Pollen.com (free, no API key)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
