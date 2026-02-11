# ve-exchange-rates

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jehg814/ve-exchange-rates/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jehg814/ve-exchange-rates/SKILL.md)
> Category: AI & LLMs

---

## Description

Get Venezuelan exchange rates - BCV official rate, Binance P2P USDT average, and the gap between them. Use when user asks for Venezuelan dollar rates, brecha cambiaria, dolar BCV, USDT P2P, or exchange rates in Venezuela.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Get Venezuelan exchange rates - BCV official rate, Binance P2P USDT average, and the gap between them. Use when user asks for Venezuelan dollar rates, brecha cambiaria, dolar BCV, USDT P2P, or exchange rates in Venezuela.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run ve-exchange-rates`)
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
You are executing the ve-exchange-rates workflow. Use the following context:

Description: Get Venezuelan exchange rates - BCV official rate, Binance P2P USDT average, and the gap between them. Use when user asks for Venezuelan dollar rates, brecha cambiaria, dolar BCV, USDT P2P, or exchange rates in Venezuela.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ve-exchange-rates
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# ve-exchange-rates: Venezuelan Exchange Rates

Get current exchange rates for Venezuela:
1. **Tasa BCV** - Official Central Bank rate
2. **Tasa USDT Binance P2P** - Average from P2P market
3. **Brecha cambiaria** - Gap between official and parallel rates

## Usage

Run the script to get current rates:

```bash
~/clawd/skills/ve-exchange-rates/scripts/get-rates.sh
```

## Output

The script returns:
- BCV official rate (Bs/USD)
- Binance P2P USDT rates (buy/sell/average)
- Gap percentage between BCV and P2P

## Data Sources

- **BCV rate**: tcambio.app or finanzasdigital.com
- **USDT P2P**: Binance P2P API (p2p.binance.com)

## Notes

- Rates are fetched in real-time from APIs
- BCV rate updates daily
- P2P rates fluctuate constantly based on market
- Script uses jq for JSON parsing

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
