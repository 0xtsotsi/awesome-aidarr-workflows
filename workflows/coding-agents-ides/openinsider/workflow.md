# openinsider

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/stuhorsman/openinsider/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/stuhorsman/openinsider/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Fetch SEC Form 4 insider trading data (Directors, CEOs, Officers) from OpenInsider. Use this to track corporate insider buying/selling signals.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Fetch SEC Form 4 insider trading data (Directors, CEOs, Officers) from OpenInsider. Use this to track corporate insider buying/selling signals.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run openinsider`)
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
You are executing the openinsider workflow. Use the following context:

Description: Fetch SEC Form 4 insider trading data (Directors, CEOs, Officers) from OpenInsider. Use this to track corporate insider buying/selling signals.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openinsider
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# OpenInsider Skill

Fetch real-time insider trading data (SEC Form 4) from OpenInsider.com.

## Usage

This skill uses a Python script to scrape and parse the OpenInsider data table.

### Get Insider Trades
Get the latest transactions for a specific ticker.

```bash
skills/openinsider/scripts/fetch_trades.py NVDA
```

### Options
- `--limit <n>`: Limit number of results (default 10)

```bash
skills/openinsider/scripts/fetch_trades.py TSLA --limit 5
```

## Output Fields

- `filing_date`: When the Form 4 was filed
- `trade_date`: When the trade happened
- `insider_name`: Name of the executive/director
- `title`: Role (CEO, CFO, Dir, etc.)
- `trade_type`: Purchase (P) or Sale (S)
- `price`: Transaction price
- `qty`: Number of shares traded
- `value`: Total value of the trade

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
