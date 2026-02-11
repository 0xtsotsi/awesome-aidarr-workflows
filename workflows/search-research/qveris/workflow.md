# qveris

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/hqman/qveris/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/hqman/qveris/SKILL.md)
> Category: Search & Research

---

## Description

Search and execute dynamic tools via QVeris API. Use when needing to find and call external APIs/tools dynamically (weather, search, data retrieval, stock trading analysis, etc.). Requires QVERIS_API_KEY environment variable.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search and execute dynamic tools via QVeris API. Use when needing to find and call external APIs/tools dynamically (weather, search, data retrieval, stock trading analysis, etc.). Requires QVERIS_API_KEY environment variable.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run qveris`)
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
You are executing the qveris workflow. Use the following context:

Description: Search and execute dynamic tools via QVeris API. Use when needing to find and call external APIs/tools dynamically (weather, search, data retrieval, stock trading analysis, etc.). Requires QVERIS_API_KEY environment variable.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: qveris
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# QVeris Tool Search & Execution

QVeris provides dynamic tool discovery and execution - search for tools by capability, then execute them with parameters.

## Setup

Requires environment variable:
- `QVERIS_API_KEY` - Get from https://qveris.ai

## Quick Start

### Search for tools
```bash
uv run scripts/qveris_tool.py search "weather forecast API"
```

### Execute a tool
```bash
uv run scripts/qveris_tool.py execute openweathermap_current_weather --search-id <id> --params '{"city": "London", "units": "metric"}'
```

## Script Usage

```
scripts/qveris_tool.py <command> [options]

Commands:
  search <query>     Search for tools matching a capability description
  execute <tool_id>  Execute a specific tool with parameters

Options:
  --limit N          Max results for search (default: 5)
  --search-id ID     Search ID from previous search (required for execute)
  --params JSON      Tool parameters as JSON string
  --max-size N       Max response size in bytes (default: 20480)
  --json             Output raw JSON instead of formatted display
```

## Workflow

1. **Search**: Describe the capability needed (not specific parameters)
   - Good: "weather forecast API"
   - Bad: "get weather for London"

2. **Select**: Review tools by `success_rate` and `avg_execution_time`

3. **Execute**: Call tool with `tool_id`, `search_id`, and `parameters`

## Example Session

```bash
# Find weather tools
uv run scripts/qveris_tool.py search "current weather data"

# Execute with returned tool_id and search_id
uv run scripts/qveris_tool.py execute openweathermap_current_weather \
  --search-id abc123 \
  --params '{"city": "Tokyo", "units": "metric"}'
```

## Use Cases

- **Weather Data**: Get current weather, forecasts for any location
- **Stock Market**: Query stock prices, historical data, earnings calendars
- **Search**: Web search, news retrieval
- **Data APIs**: Currency exchange, geolocation, translations
- **And more**: QVeris aggregates thousands of API tools

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
