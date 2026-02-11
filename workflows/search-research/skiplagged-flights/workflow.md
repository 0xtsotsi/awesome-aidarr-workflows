# skiplagged-flights

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/wzs/skiplagged-flights/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/wzs/skiplagged-flights/SKILL.md)
> Category: Search & Research

---

## Description

Search cheapest flights via Skiplagged MCP. Use for flight deals, price comparison, flexible dates, and destination discovery.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search cheapest flights via Skiplagged MCP. Use for flight deals, price comparison, flexible dates, and destination discovery.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run skiplagged-flights`)
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
You are executing the skiplagged-flights workflow. Use the following context:

Description: Search cheapest flights via Skiplagged MCP. Use for flight deals, price comparison, flexible dates, and destination discovery.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: skiplagged-flights
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Skiplagged Flights

Search flights using Skiplagged MCP via mcporter.

## Quick Start

```bash
mcporter call skiplagged.sk_flights_search origin=WAW destination=LHR departureDate=2026-02-15
```

## Tools

### sk_flights_search
Search flights between locations.

**Required:** `origin`, `destination`, `departureDate`

**Common options:**
- `returnDate` - Round-trip date
- `sort` - `price`, `duration`, `value` (default)
- `limit` - Max results (default 12)
- `maxStops` - `none`, `one`, `many`
- `fareClass` - `basic-economy`, `economy`, `premium`, `business`, `first`
- `preferredAirlines`/`excludedAirlines` - e.g., `['UA','DL']`
- `departureTimeEarliest`/`departureTimeLatest` - Minutes from midnight (0-1439)

**Examples:**
```bash
# Cheapest one-way
mcporter call skiplagged.sk_flights_search origin=NYC destination=LAX departureDate=2026-03-15 sort=price

# Round-trip, nonstop only
mcporter call skiplagged.sk_flights_search origin=WAW destination=CDG departureDate=2026-04-10 returnDate=2026-04-17 maxStops=none

# Exclude budget airlines, morning only (6am-12pm)
mcporter call skiplagged.sk_flights_search origin=LHR destination=JFK departureDate=2026-05-01 excludedAirlines=F9,NK departureTimeEarliest=360 departureTimeLatest=720
```

### sk_flex_departure_calendar
Find cheapest fares around a departure date.

```bash
mcporter call skiplagged.sk_flex_departure_calendar origin=WAW destination=BCN departureDate=2026-06-15 sort=price
```

### sk_flex_return_calendar
Find cheapest round-trip fares for fixed trip length.

```bash
mcporter call skiplagged.sk_flex_return_calendar origin=WAW destination=NYC departureDate=2026-07-01 returnDate=2026-07-08
```

### sk_destinations_anywhere
Discover cheap destinations when flexible.

```bash
mcporter call skiplagged.sk_destinations_anywhere from=WAW depart=2026-02-15
```

## Response Formatting

When presenting flight results to users:

- **NEVER use markdown tables** - use bullet lists or labeled lines instead
- Use **MarkdownV2** compatible formatting (Telegram-safe)
- Keep replies **mobile-friendly** - concise, scannable
- **Limit results** shown (top 3-5), offer more if needed

**Good example:**
```
Found 3 flights WAW → LHR on Feb 15:

• $90 · 28h 15m · 1 stop
  Wizz Air + SAS
  05:40 WAW → 08:55+1 LHR
  [Book](link)

• $91 · 12h 20m · 1 stop
  Wizz Air + SAS  
  05:40 WAW → 17:00 LHR
  [Book](link)
```

## Tips

- Use IATA codes (e.g., `WAW`, `LHR`, `JFK`)
- Hidden city flights included by default (often cheapest)
- Add `--output json` for structured data
- Results include `deepLink` for booking

## References

- Tool schemas: `mcporter list skiplagged --schema`
- MCP docs: https://skiplagged.github.io/mcp/

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
