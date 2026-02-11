# quodd

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/khaney64/quodd/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/khaney64/quodd/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Fetch real-time stock quotes via Quodd API. Get current prices, daily high/low, and after-hours data for US equities. Use when the user asks for stock prices, quotes, market data, or ticker information.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Fetch real-time stock quotes via Quodd API. Get current prices, daily high/low, and after-hours data for US equities. Use when the user asks for stock prices, quotes, market data, or ticker information.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run quodd`)
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
You are executing the quodd workflow. Use the following context:

Description: Fetch real-time stock quotes via Quodd API. Get current prices, daily high/low, and after-hours data for US equities. Use when the user asks for stock prices, quotes, market data, or ticker information.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: quodd
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Quodd Stock Quotes

Fetch real-time stock quotes for US equities via the Quodd API.

For more information, visit: https://www.quodd.com/stock-and-etf-data

## Quick Start

```bash
# Get a quote for Apple
python scripts/quote.py AAPL

# Get quotes for multiple tickers
python scripts/quote.py AAPL MSFT META
```

## Prerequisites

Set the following environment variables:

```bash
export QUODD_USERNAME="your_username"
export QUODD_PASSWORD="your_password"
```

## Usage

### Single Ticker

```bash
python scripts/quote.py AAPL
```

### Multiple Tickers

```bash
python scripts/quote.py AAPL MSFT META GOOGL
```

### JSON Output

```bash
python scripts/quote.py AAPL --format json
```

### Force Token Refresh

```bash
python scripts/quote.py AAPL --no-cache
```

## Output Format

### Text (Default)

```
Quodd Stock Quotes
Symbol   Date        Time      High      Low     Close    AH Time     AH Price
-------------------------------------------------------------------------------
AAPL     01/29/26    14:30    185.50   180.25   182.63   17:45:30     182.80
```

### JSON

```json
{
  "quotes": [
    {
      "symbol": "AAPL",
      "date": "01/29/26",
      "time": "14:30",
      "high": 185.50,
      "low": 180.25,
      "close": 182.63,
      "after_hours_time": "17:45:30",
      "after_hours_price": 182.80
    }
  ]
}
```

## Output Fields

- **Symbol** - Stock ticker symbol
- **Date** - Quote date
- **Time** - Quote time
- **High** - Day high price
- **Low** - Day low price
- **Close** - Last traded price
- **AH Time** - After hours trade time
- **AH Price** - After hours price

## Notes

- Authentication tokens are cached at `~/.openclaw/credentials/quodd-token.json` for 20 hours
- Use `--no-cache` if you encounter authentication errors after credential changes

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
