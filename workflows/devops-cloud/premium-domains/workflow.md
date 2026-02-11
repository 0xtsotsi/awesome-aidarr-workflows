# premium-domains

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/julianengel/premium-domains/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/julianengel/premium-domains/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Search for premium domains for sale across Afternic, Sedo, Atom, Dynadot, Namecheap, NameSilo, and Unstoppable Domains.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search for premium domains for sale across Afternic, Sedo, Atom, Dynadot, Namecheap, NameSilo, and Unstoppable Domains.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run premium-domains`)
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
You are executing the premium-domains workflow. Use the following context:

Description: Search for premium domains for sale across Afternic, Sedo, Atom, Dynadot, Namecheap, NameSilo, and Unstoppable Domains.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: premium-domains
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Premium Domain Search

Find domains for sale across major marketplaces. Free API, just curl.

## Usage

```bash
curl -s "https://api.domaindetails.com/api/marketplace/search?domain=example.com" | jq
```

## Marketplaces Checked

- **Afternic** — GoDaddy's premium marketplace
- **Sedo** — Global domain trading platform
- **Atom** — Premium domain marketplace
- **Dynadot** — Auctions & buy-now listings
- **Namecheap** — Integrated registrar marketplace
- **NameSilo** — Budget-friendly marketplace
- **Unstoppable Domains** — Web3 domains

## Response Fields

- `found` — whether any listings exist
- `marketplaces.<name>.listing.price` — price in cents or dollars
- `marketplaces.<name>.listing.currency` — USD, EUR, etc.
- `marketplaces.<name>.listing.url` — direct link to listing
- `marketplaces.<name>.listing.listingType` — buy_now, auction, make_offer

## Rate Limits

- 100 requests/minute (no auth needed)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
