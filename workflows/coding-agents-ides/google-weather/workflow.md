# google-weather

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/shaharsha/google-weather/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/shaharsha/google-weather/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Google Weather API - accurate, real-time weather data. Get current conditions, temperature, humidity, wind, and forecasts. Powered by Google's Weather API for reliable, hyperlocal data updated every 15 minutes. Supports any location worldwide.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** weather, google, forecast, temperature, real-time, current-conditions, climate, wind, humidity

---

## GOTCHA Framework

### G - Goals
Google Weather API - accurate, real-time weather data. Get current conditions, temperature, humidity, wind, and forecasts. Powered by Google's Weather API for reliable, hyperlocal data updated every 15 minutes. Supports any location worldwide.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run google-weather`)
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
You are executing the google-weather workflow. Use the following context:

Description: Google Weather API - accurate, real-time weather data. Get current conditions, temperature, humidity, wind, and forecasts. Powered by Google's Weather API for reliable, hyperlocal data updated every 15 minutes. Supports any location worldwide.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: google-weather
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Google Weather - Real-time Weather Data

Get accurate weather conditions using Google's Weather API. Requires a Google Cloud API key with Weather API enabled.

## Quick Usage

```bash
# Current weather (formatted output)
python3 skills/google-weather/lib/weather_helper.py current "New York"
python3 skills/google-weather/lib/weather_helper.py current "London"
python3 skills/google-weather/lib/weather_helper.py current "Sydney"

# 24h Forecast
python3 skills/google-weather/lib/weather_helper.py forecast "Tel Aviv"

# Raw JSON data
python3 skills/google-weather/lib/weather_helper.py json "Paris"
```

## Example Output

```
*New York*
Partly Cloudy ⛅
🌡️ 12°C (feels like 10°C)
💨 Wind: 18 km/h NORTHWEST
💧 Humidity: 55%
```

```
*24h Forecast for Tel Aviv*
18:00: 17.8°C, ☀️ 5 km/h NORTH
22:00: 14.3°C, ☀️ 6 km/h EAST_NORTHEAST
02:00: 12.8°C, ⛅ 8 km/h NORTHEAST
06:00: 10.8°C, ☀️ 6 km/h EAST_NORTHEAST
10:00: 16.1°C, ☀️ 5 km/h SOUTH
14:00: 20.4°C, 🌤️ 8 km/h WEST_NORTHWEST
```

## Supported Locations

Any location worldwide - just type the city name:
- `New York`, `London`, `Paris`, `Berlin`, `Sydney`
- `San Francisco`, `Berlin`, `Singapore`, `Dubai`
- Or any address, landmark, or coordinates

The skill automatically geocodes locations using Google Maps API.

## Data Available

- **Temperature**: Current + feels like
- **Conditions**: Clear, cloudy, rain, snow, etc. with emoji icons
- **Forecast**: Hourly data for temperature, wind, and conditions
- **Humidity**: Percentage
- **Wind**: Speed, direction, gusts
- **UV Index**: Sun exposure level
- **Precipitation**: Probability and type
- **Cloud Cover**: Percentage
- **Visibility**: Distance

## Setup

1. Create a project in [Google Cloud Console](https://console.cloud.google.com/)
2. Enable the [Weather API](https://console.cloud.google.com/apis/library/weather.googleapis.com)
3. Enable the [Geocoding API](https://console.cloud.google.com/apis/library/geocoding-backend.googleapis.com) (for location name lookup)
4. Create an API key and set it as `GOOGLE_API_KEY` environment variable

> Also supports `GOOGLE_WEATHER_API_KEY` or `GOOGLE_MAPS_API_KEY` if you already have one configured.

## Multi-language Support

Output adapts to location - supports English, Hebrew, and other languages based on the `language` parameter.

```bash
# Hebrew output
python3 skills/google-weather/lib/weather_helper.py current "Tel Aviv"
# Output: בהיר ☀️ 19°C...
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
