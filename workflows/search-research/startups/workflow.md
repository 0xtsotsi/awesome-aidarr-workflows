# startups

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/networkingit/startups/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/networkingit/startups/SKILL.md)
> Category: Search & Research

---

## Description

Research startups, funding rounds, acquisitions, and hiring trends via startups.in

**Homepage:** https://startups.in
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Research startups, funding rounds, acquisitions, and hiring trends via startups.in

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run startups`)
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
You are executing the startups workflow. Use the following context:

Description: Research startups, funding rounds, acquisitions, and hiring trends via startups.in

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: startups
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: https://startups.in
```

---

## Original Skill Content



# startups.in Startup Research

Research startups, track funding, and discover hiring trends using startups.in.

## Capabilities

- **Search** - Find startups by name, sector, location
- **Details** - Get comprehensive startup info
- **Funding** - Track rounds, valuations, investors
- **Hiring** - Monitor job postings and team growth
- **Compare** - Side-by-side comparisons

## Example Queries

- "Find AI startups in San Francisco"
- "Tell me about Stripe"
- "What's Anthropic's latest funding?"
- "Is Vercel hiring?"
- "Compare Notion and Coda"

## API

Base URL: `https://startups.in`

### Search
```http
GET /api/search?q={query}
```

### Get Startup
```http
GET /api/startups/{slug}
```

### Get Jobs
```http
GET /api/startups/{slug}/jobs
```

### Compare
```http
GET /api/compare?startups={slug1},{slug2}
```

## Authentication

Public access works without auth. For enhanced access, use Moltbook identity:

```http
X-Moltbook-Identity: {token}
```

## Links

- Website: https://startups.in
- Moltbook: https://moltbook.com/u/startups

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
