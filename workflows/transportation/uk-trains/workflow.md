# uk-trains

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jabbslad/uk-trains/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jabbslad/uk-trains/SKILL.md)
> Category: Transportation

---

## Description

Query UK National Rail live departure boards, arrivals, delays, and train services. Use when asked about train times, departures, arrivals, delays, platforms, or "when is the next train" for UK railways. Supports all GB stations via Darwin/Huxley2 API.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Query UK National Rail live departure boards, arrivals, delays, and train services. Use when asked about train times, departures, arrivals, delays, platforms, or "when is the next train" for UK railways. Supports all GB stations via Darwin/Huxley2 API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run uk-trains`)
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
You are executing the uk-trains workflow. Use the following context:

Description: Query UK National Rail live departure boards, arrivals, delays, and train services. Use when asked about train times, departures, arrivals, delays, platforms, or "when is the next train" for UK railways. Supports all GB stations via Darwin/Huxley2 API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: uk-trains
category: Transportation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# UK Trains

Query National Rail Darwin API for live train departures and arrivals.

## Setup

Requires free Darwin API token:
1. Register at https://realtime.nationalrail.co.uk/OpenLDBWSRegistration/
2. Set `NATIONAL_RAIL_TOKEN` in environment (or configure in skills.entries.uk-trains.apiKey)

## Commands

```bash
# Departures
./scripts/trains.py departures PAD
./scripts/trains.py departures PAD to OXF --rows 5

# Arrivals  
./scripts/trains.py arrivals MAN
./scripts/trains.py arrivals MAN from EUS

# Station search
./scripts/trains.py search paddington
./scripts/trains.py search kings
```

## Station Codes

Use 3-letter CRS codes:
- `PAD` = London Paddington
- `EUS` = London Euston  
- `KGX` = London Kings Cross
- `VIC` = London Victoria
- `WAT` = London Waterloo
- `MAN` = Manchester Piccadilly
- `BHM` = Birmingham New Street
- `EDB` = Edinburgh Waverley
- `GLC` = Glasgow Central
- `BRI` = Bristol Temple Meads
- `LDS` = Leeds
- `LIV` = Liverpool Lime Street
- `RDG` = Reading
- `OXF` = Oxford
- `CBG` = Cambridge

## Response Format

JSON with:
- `locationName`, `crs` - Station info
- `messages[]` - Service alerts
- `trainServices[]` - List of trains:
  - `std`/`sta` - Scheduled departure/arrival time
  - `etd`/`eta` - Expected time ("On time", "Delayed", or actual time)
  - `platform` - Platform number
  - `operator` - Train operating company
  - `destination[].name` - Final destination
  - `isCancelled`, `cancelReason`, `delayReason` - Disruption info

## Message Template

Use this compact format for WhatsApp/chat responses:

```
🚂 {Origin} → {Destination}

*{dep} → {arr}* │📍{platform} │ 🚃 {coaches}
{status}

*{dep} → {arr}* │📍{platform} │ 🚃 {coaches}
{status}
```

### Elements
- **Header:** 🚂 emoji + origin → destination
- **Time:** Bold, departure → arrival times
- **Platform:** 📍 + number (or "TBC" if unknown)
- **Coaches:** 🚃 + space + number
- **Status:**
  - ✅ On time
  - ⚠️ Delayed (exp {time})
  - ❌ Cancelled — {reason}
  - 🔄 Starts here

### Example

```
🚂 Hemel Hempstead → Euston

*20:18 → 20:55* │📍4 │ 🚃 4
✅ On time

*20:55 → 21:30* │📍4 │ 🚃 12
✅ On time

*21:11 → 21:41* │📍4 │ 🚃 8
✅ On time
```

### Getting Arrival Times
To show arrival times, make two API calls:
1. `departures {origin} to {dest}` — get departure times + service IDs
2. `arrivals {dest} from {origin}` — get arrival times

Match services by the numeric prefix in serviceID (e.g., `4748110HEMLHMP_` matches `4748110EUSTON__`).

### Notes
- Separate each service with a blank line
- Omit coaches if formation data unavailable
- For delays, show expected time: `⚠️ Delayed (exp 20:35)`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
