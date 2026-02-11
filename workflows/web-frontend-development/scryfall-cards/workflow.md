# scryfall-cards

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/santidev95/scryfall-cards/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/santidev95/scryfall-cards/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Search and retrieve Magic: The Gathering card data using the Scryfall API. Use this skill when the user asks about MTG cards, wants to search for cards by name, type, color, mana cost, oracle text, set, or any other card attribute. Also use for getting card images, prices, rulings, legality information, or random cards. Triggers include mentions of MTG, Magic, Magic: The Gathering, card names, deck building questions, or requests for card information.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search and retrieve Magic: The Gathering card data using the Scryfall API. Use this skill when the user asks about MTG cards, wants to search for cards by name, type, color, mana cost, oracle text, set, or any other card attribute. Also use for getting card images, prices, rulings, legality information, or random cards. Triggers include mentions of MTG, Magic, Magic: The Gathering, card names, deck building questions, or requests for card information.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run scryfall-cards`)
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
You are executing the scryfall-cards workflow. Use the following context:

Description: Search and retrieve Magic: The Gathering card data using the Scryfall API. Use this skill when the user asks about MTG cards, wants to search for cards by name, type, color, mana cost, oracle text, set, or any other card attribute. Also use for getting card images, prices, rulings, legality information, or random cards. Triggers include mentions of MTG, Magic, Magic: The Gathering, card names, deck building questions, or requests for card information.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: scryfall-cards
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Scryfall MTG Card Search

Search for Magic: The Gathering cards using the Scryfall API.

## API Overview

Base URL: `https://api.scryfall.com`

**Required Headers:**
```python
headers = {
    "User-Agent": "OpenClawMTGSkill/1.0",
    "Accept": "application/json"
}
```

**Rate Limiting:** Insert 50-100ms delay between requests (max 10 req/sec).

## Core Endpoints

### Search Cards
```
GET /cards/search?q={query}
```

Parameters:
- `q` (required): Fulltext search query
- `unique`: cards|art|prints (default: cards)
- `order`: name|set|released|rarity|color|usd|tix|eur|cmc|power|toughness|edhrec|penny|artist|review
- `dir`: auto|asc|desc
- `page`: Page number for pagination

### Named Card Lookup
```
GET /cards/named?exact={name}
GET /cards/named?fuzzy={name}
```

Use `fuzzy` for partial matches (e.g., "jac bele" → "Jace Beleren").
Add `&set={code}` to limit to specific set.

### Random Card
```
GET /cards/random
GET /cards/random?q={query}
```

### Card by ID
```
GET /cards/{id}
GET /cards/{set_code}/{collector_number}
```

### Autocomplete
```
GET /cards/autocomplete?q={partial_name}
```

Returns up to 20 card name suggestions.

## Search Syntax Reference

See `references/search_syntax.md` for the complete search syntax guide.

**Quick examples:**
- `c:red pow=3` - Red cards with power 3
- `t:merfolk t:legend` - Legendary merfolk
- `o:"draw a card"` - Cards with "draw a card" in text
- `cmc=3 r:rare` - 3-mana rares
- `e:dom` - Cards from Dominaria
- `f:standard` - Standard legal cards
- `usd<1` - Cards under $1

## Implementation

Use the provided script for common operations:

```bash
python3 scripts/scryfall_search.py search "lightning bolt"
python3 scripts/scryfall_search.py named --exact "Black Lotus"
python3 scripts/scryfall_search.py random
python3 scripts/scryfall_search.py random --query "t:dragon"
```

Or make direct API calls with proper headers and rate limiting.

## Card Object Key Fields

When displaying card info, prioritize these fields:
- `name`, `mana_cost`, `type_line`
- `oracle_text`, `power`, `toughness`
- `image_uris.normal` (for card image)
- `prices.usd`, `prices.usd_foil`
- `legalities` (format legality)
- `set_name`, `rarity`

For double-faced cards, check `card_faces` array.

## Error Handling

- 404: Card not found
- 422: Invalid search query
- 429: Rate limited (wait and retry)

Always validate responses have `object` field; if `object: "error"`, check `details` for message.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
