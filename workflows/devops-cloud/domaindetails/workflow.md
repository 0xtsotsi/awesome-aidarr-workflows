# domaindetails

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/julianengel/domaindetails/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/julianengel/domaindetails/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Look up domain WHOIS/RDAP info and check marketplace listings. Free API, no auth required.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Look up domain WHOIS/RDAP info and check marketplace listings. Free API, no auth required.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run domaindetails`)
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
You are executing the domaindetails workflow. Use the following context:

Description: Look up domain WHOIS/RDAP info and check marketplace listings. Free API, no auth required.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: domaindetails
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# domaindetails

Domain lookup and marketplace search. Free API, just curl.

## Domain Lookup

```bash
curl -s "https://mcp.domaindetails.com/lookup/example.com" | jq
```

Returns: registrar, created/expires dates, nameservers, DNSSEC, contacts.

## Marketplace Search

```bash
curl -s "https://api.domaindetails.com/api/marketplace/search?domain=example.com" | jq
```

Returns listings from: Sedo, Afternic, Atom, Dynadot, Namecheap, NameSilo, Unstoppable Domains.

## Rate Limits

- 100 requests/minute (no auth needed)

## CLI (Optional)

```bash
npx domaindetails example.com
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
