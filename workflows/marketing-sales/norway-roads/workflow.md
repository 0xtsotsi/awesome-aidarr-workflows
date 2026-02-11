# norway-roads

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/geoffreycasaubon/norway-roads/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/geoffreycasaubon/norway-roads/SKILL.md)
> Category: Marketing & Sales

---

## Description

Query real-time road conditions, closures, and traffic issues in Norway. Use when the user asks about road status, closed roads, traffic conditions, weather on roads, or planning a route in Norway. Handles queries like "Are there road closures between Oslo and Bergen?", "What's the road condition on E6?", "Any issues driving to Trondheim today?", or general road condition checks for Norwegian roads.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Query real-time road conditions, closures, and traffic issues in Norway. Use when the user asks about road status, closed roads, traffic conditions, weather on roads, or planning a route in Norway. Handles queries like "Are there road closures between Oslo and Bergen?", "What's the road condition on E6?", "Any issues driving to Trondheim today?", or general road condition checks for Norwegian roads.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run norway-roads`)
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
You are executing the norway-roads workflow. Use the following context:

Description: Query real-time road conditions, closures, and traffic issues in Norway. Use when the user asks about road status, closed roads, traffic conditions, weather on roads, or planning a route in Norway. Handles queries like "Are there road closures between Oslo and Bergen?", "What's the road condition on E6?", "Any issues driving to Trondheim today?", or general road condition checks for Norwegian roads.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: norway-roads
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Norway Roads

Query real-time road closures and conditions from Statens Vegvesen NVDB API.

## Quick Start

Check all current road closures:
```bash
./scripts/query_roads.py
```

Check route between two cities:
```bash
./scripts/query_roads.py --from Oslo --to Bergen
```

Check specific road/location:
```bash
./scripts/query_roads.py --road "Strynefjell"
```

Get JSON output:
```bash
./scripts/query_roads.py --json
```

## Usage Examples

### Check Route Conditions

When planning a trip between two Norwegian cities:

```bash
./scripts/query_roads.py --from Oslo --to Bergen
./scripts/query_roads.py --from Oslo --to Trondheim
./scripts/query_roads.py --from Bergen --to Stavanger
```

Supported cities: Oslo, Bergen, Stavanger, Trondheim, Tromsø, Kristiansand, Ålesund, Bodø

### Filter by Location Name

```bash
./scripts/query_roads.py --road "Strynefjell"
./scripts/query_roads.py --road "E6"
```

## What Data is Returned

The skill queries two types of road restrictions from NVDB:

1. **Vegstengning (Road Closures)** - Scheduled or permanent closures
   - Seasonal closures (winter mountain passes)
   - Landslide/avalanche closures
   - Maintenance closures
   - Causes: Snow (Snø), Ice (Is), Rock (Stein)

2. **Vegsperring (Physical Barriers)** - Physical blocking of roads
   - Gates, barriers, concrete blocks
   - Permanent restrictions

## API Response Format

Each closure includes:
- **location**: Street/road name
- **county**: Norwegian county (fylke)
- **municipality**: Kommune
- **from_date/to_date**: Closure period
- **cause**: Reason (Snø=snow, Is=ice, Stein=rock)
- **type**: closure or barrier

## Data Source

- **API**: NVDB v3 (Nasjonal VegDataBank)
- **URL**: https://nvdbapiles-v3.atlas.vegvesen.no
- **Object types**: 485 (Vegstengning), 607 (Vegsperring)
- **Update frequency**: Real-time from official database
- **No API key required**: Open public data

## Common Norwegian Terms

| Norwegian | English |
|-----------|---------|
| Vegstengning | Road closure |
| Vegsperring | Road barrier |
| Snø | Snow |
| Is | Ice |
| Stein | Rock |
| Fylke | County |
| Stengt | Closed |

## Major Routes & Counties

**Counties (Fylker):**
- Viken (Oslo region)
- Vestland (Bergen region)
- Rogaland (Stavanger region)
- Trøndelag (Trondheim region)
- Troms og Finnmark (North)
- Agder (South)
- Møre og Romsdal (Ålesund region)
- Nordland (Bodø region)

**Major Roads:**
- E6: North-south trunk (Kirkenes-Halden)
- E16: Bergen-Oslo via Lærdal tunnel
- E39: West coast route

## Limitations

- Shows registered closures in NVDB, not real-time traffic incidents
- For live traffic, use Vegvesen mobile app or call 175
- Winter closures are often seasonal and recurring
- Some recent incidents may not yet be registered

## Reference

See [references/api-docs.md](references/api-docs.md) for API details and city mappings.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
