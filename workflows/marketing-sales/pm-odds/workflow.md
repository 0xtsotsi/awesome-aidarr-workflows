# pm-odds

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dannyshmueli/pm-odds/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dannyshmueli/pm-odds/SKILL.md)
> Category: Marketing & Sales

---

## Description

Query Polymarket prediction markets. Use for questions about prediction markets, betting odds, market prices, event probabilities, or when user asks about Polymarket data.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Query Polymarket prediction markets. Use for questions about prediction markets, betting odds, market prices, event probabilities, or when user asks about Polymarket data.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run pm-odds`)
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
You are executing the pm-odds workflow. Use the following context:

Description: Query Polymarket prediction markets. Use for questions about prediction markets, betting odds, market prices, event probabilities, or when user asks about Polymarket data.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: pm-odds
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Polymarket

Query prediction market data from Polymarket's public API (no auth required).

## Quick Start

```bash
# Top markets by 24h volume
python3 scripts/polymarket.py --top

# Search markets
python3 scripts/polymarket.py --search "trump"

# Get specific market by slug
python3 scripts/polymarket.py --slug "will-trump-win-the-2024-election"

# List events (grouped markets)
python3 scripts/polymarket.py --events
```

## Script Location

`skills/polymarket/scripts/polymarket.py`

## API Endpoints

The script uses `gamma-api.polymarket.com`:
- `/markets` - Individual markets with prices, volumes
- `/events` - Event groups containing related markets

## Output Format

Markets show: question, Yes/No prices (as percentages), 24h volume, total volume.

## Interpreting Prices

- `outcomePrices` are 0-1 representing probability
- Price of 0.65 for "Yes" = market thinks 65% chance of Yes
- Higher volume = more liquid, more reliable signal

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
