# Domain Hunter Workflow

**Status:** Active
**Date:** 2026-02-21
**Use Case:** Find and purchase domain names at the best price
**Source:** Adapted from OPC Skills (resciencelab/opc-skills)

## Overview

Search domains, compare prices across registrars, find promo codes, and get purchase recommendations.

## ATLAS Alignment

| ATLAS Phase | Workflow Step |
|-------------|---------------|
| Architect | Generate domain ideas based on project |
| Trace | Check availability via WHOIS |
| Link | Connect to registrars, compare prices |
| Assemble | Find promo codes, build comparison |
| Stress-test | Verify final recommendation |

## Trigger

This workflow is invoked when user mentions:
- Buy domain, check domain prices
- Domain deals, compare registrars
- Search for .ai/.com domains

## Workflow Steps

### Phase 1: Architect (Generate Ideas)

Generate 5-10 creative domain name suggestions:

**Guidelines:**
- Keep names short (under 15 characters)
- Make them memorable and brandable
- Common suffixes: app, io, hq, ly, ify, now, hub
- Patterns: `{action}{noun}`, `{noun}{suffix}`, `{prefix}{keyword}`

### Phase 2: Trace (Check Availability)

**CRITICAL: Always check availability before presenting!**

```bash
# WHOIS check (most reliable)
whois {domain}.{tld} 2>/dev/null | grep -i "no match\|not found\|available" && echo "AVAILABLE" || echo "TAKEN"
```

**Alternative:**
```bash
open "https://www.spaceship.com/domains/?search={domain}.{tld}"
```

**Only present domains that are confirmed AVAILABLE**

### Phase 3: Link (Compare Prices)

Use WebSearch to find current prices:
```
WebSearch: "cheapest .{tld} domain registrar 2026 site:tld-list.com"
```

**Price comparison sites:**
- tld-list.com/tld/{tld}
- tldes.com/{tld}

### Phase 4: Assemble (Find Deals)

**Search for promo codes via Twitter:**
```bash
python3 <twitter_skill>/scripts/search_tweets.py "from:{registrar} promo code" --type Latest --limit 15
```

**Search Reddit:**
```bash
python3 <reddit_skill>/scripts/search_posts.py "{registrar} promo code" --limit 15
```

**Major registrars:** Spaceship, Dynadot, Namecheap, Porkbun, Cloudflare

### Phase 5: Stress-Test (Recommend)

Present final recommendation:
```markdown
## Recommendation

**Domain:** example.ai
**Best Registrar:** Spaceship
**Price:** $68.98/year (2-year minimum)
**Promo Code:** None for .ai
**Purchase Link:** https://www.spaceship.com/

### Price Comparison
| Registrar | Year 1 | Renewal | 2-Year Total |
|-----------|--------|---------|--------------|
| Spaceship | $68.98 | $68.98  | $137.96      |
| Cloudflare| $70.00 | $70.00  | $140.00      |
```

## Important Notes

1. **Premium TLDs** (.ai, .io) rarely have promo codes
2. **.ai domains** require 2-year minimum
3. **Cloudflare** offers at-cost pricing
4. **Renewal prices** often differ from registration
5. **WHOIS privacy** is free at most registrars

## References

- [references/registrars.md](./references/registrars.md) - Detailed registrar comparison
