# trein

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/joehoel/trein/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/joehoel/trein/SKILL.md)
> Category: Transportation

---

## Description

Query Dutch Railways (NS) for train departures, trip planning, disruptions, and station search via the trein CLI.

**Homepage:** https://github.com/joelkuijper/trein
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Query Dutch Railways (NS) for train departures, trip planning, disruptions, and station search via the trein CLI.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run trein`)
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
You are executing the trein workflow. Use the following context:

Description: Query Dutch Railways (NS) for train departures, trip planning, disruptions, and station search via the trein CLI.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: trein
category: Transportation
version: 1.0.0
user_invocable: True
homepage: https://github.com/joelkuijper/trein
```

---

## Original Skill Content



# trein - Dutch Railways CLI

A CLI for the NS (Dutch Railways) API with real-time departures, trip planning, disruptions, and station search.

## Install

npm (recommended):
```bash
npm i -g trein
```

Or download a standalone binary from [GitHub Releases](https://github.com/joelkuijper/trein/releases).

## Setup

Get an API key from https://apiportal.ns.nl/ and set it:
```bash
export NS_API_KEY="your-api-key"
```

Or create `~/.config/trein/trein.config.json`:
```json
{ "apiKey": "your-api-key" }
```

## Commands

### Departures
```bash
trein departures "Amsterdam Centraal"
trein d amsterdam
trein d amsterdam --json  # structured output
```

### Trip Planning
```bash
trein trip "Utrecht" "Den Haag Centraal"
trein t utrecht denhaag --json
```

### Disruptions
```bash
trein disruptions
trein disruptions --json
```

### Station Search
```bash
trein stations rotterdam
trein s rotterdam --json
```

### Aliases (shortcuts)
```bash
trein alias set home "Amsterdam Centraal"
trein alias set work "Rotterdam Centraal"
trein alias list
trein d home  # uses alias
```

## Tips
- Use `--json` flag for all commands to get structured output for parsing
- Station names support fuzzy matching (e.g., "adam" -> "Amsterdam Centraal")
- Aliases are stored in the config file and can be used in place of station names

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
