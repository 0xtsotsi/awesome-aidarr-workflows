# polymarket

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mvanhorn/polymarket/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mvanhorn/polymarket/SKILL.md)
> Category: Marketing & Sales

---

## Description

Query Polymarket prediction markets - check odds, trending markets, search events, track prices.

**Homepage:** https://polymarket.com
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Query Polymarket prediction markets - check odds, trending markets, search events, track prices.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run polymarket`)
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
You are executing the polymarket workflow. Use the following context:

Description: Query Polymarket prediction markets - check odds, trending markets, search events, track prices.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: polymarket
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: https://polymarket.com
```

---

## Original Skill Content



# Polymarket

Query [Polymarket](https://polymarket.com) prediction markets. Check odds, find trending markets, search events.

## Commands

```bash
# Trending/active markets
python3 {baseDir}/scripts/polymarket.py trending

# Search markets
python3 {baseDir}/scripts/polymarket.py search "trump"
python3 {baseDir}/scripts/polymarket.py search "bitcoin"

# Get specific market by slug
python3 {baseDir}/scripts/polymarket.py event "fed-decision-in-october"

# Get markets by category
python3 {baseDir}/scripts/polymarket.py category politics
python3 {baseDir}/scripts/polymarket.py category crypto
python3 {baseDir}/scripts/polymarket.py category sports
```

## Example Chat Usage

- "What are the odds Trump wins 2028?"
- "Trending on Polymarket?"
- "Search Polymarket for Bitcoin"
- "What's the spread on the Fed rate decision?"
- "Any interesting crypto markets?"

## Output

Markets show:
- Question/title
- Current odds (Yes/No prices)
- Volume
- End date

## API

Uses the public Gamma API (no auth required for reading):
- Base URL: `https://gamma-api.polymarket.com`
- Docs: https://docs.polymarket.com

## Note

This is read-only. Trading requires wallet authentication (not implemented).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
