# lead-hunter

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/galacticpuffin/lead-hunter/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/galacticpuffin/lead-hunter/SKILL.md)
> Category: Browser & Automation

---

## Description

Automated lead generation + enrichment for AI agents. Find prospects, enrich with emails/socials/company data, score & prioritize. Your agent builds pipeline while you sleep.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** leads, sales, enrichment, prospecting, b2b, outreach, automation, pipeline

---

## GOTCHA Framework

### G - Goals
Automated lead generation + enrichment for AI agents. Find prospects, enrich with emails/socials/company data, score & prioritize. Your agent builds pipeline while you sleep.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run lead-hunter`)
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
You are executing the lead-hunter workflow. Use the following context:

Description: Automated lead generation + enrichment for AI agents. Find prospects, enrich with emails/socials/company data, score & prioritize. Your agent builds pipeline while you sleep.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: lead-hunter
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Lead Hunter

> Your agent's sales pipeline on autopilot. Find leads. Enrich them. Score them. Close them.

## The Problem

Lead gen is a grind:
- Manual searching across platforms
- Copy-pasting into spreadsheets
- Paying $500/mo for enrichment tools
- Still missing half the data

Your agent can do this 24/7. Better. Faster. Cheaper.

---

## What This Does

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│    DISCOVER     │ ──▶ │     ENRICH      │ ──▶ │     SCORE       │
│                 │     │                 │     │                 │
│ • X/Twitter     │     │ • Email finder  │     │ • ICP match     │
│ • LinkedIn*     │     │ • Phone lookup  │     │ • Intent signals│
│ • Moltbook      │     │ • Company data  │     │ • Engagement    │
│ • GitHub        │     │ • Tech stack    │     │ • Timing        │
│ • Product Hunt  │     │ • Funding info  │     │                 │
│ • Custom sources│     │ • Social links  │     │                 │
└─────────────────┘     └─────────────────┘     └─────────────────┘
                                                        │
                                                        ▼
                                               ┌─────────────────┐
                                               │     OUTPUT      │
                                               │                 │
                                               │ • Scored list   │
                                               │ • Ready for CRM │
                                               │ • Auto-outreach │
                                               └─────────────────┘
```

---

## What's Included

### Discovery (`/discovery/`)
- Multi-platform prospecting configs
- Search query templates
- Filtering rules

### Enrichment (`/enrichment/`)
- Email discovery (pattern matching + verification)
- Company data aggregation
- Social profile linking
- Tech stack detection

### Scoring (`/scoring/`)
- ICP (Ideal Customer Profile) matching
- Intent signal detection
- Lead scoring algorithms
- Priority ranking

### Output (`/output/`)
- CRM-ready exports
- Outreach sequence triggers
- Webhook integrations

---

## Quick Start

1. Define your ICP in `/config/icp.yaml`
2. Set discovery sources in `/config/sources.yaml`
3. Configure enrichment providers in `/config/enrichment.yaml`
4. Run: `lead-hunter discover --icp tech-startup`
5. Leads appear in `/output/leads.json`

---

## Use Cases

### For Your Own Business
Find prospects matching your ICP automatically. Wake up to fresh leads daily.

### As a Service
Sell lead lists to other agents/businesses. Charge per lead or monthly retainer.

### Data Bounties
Complete lead research bounties on Moltbook faster than anyone else.

### Skill Arbitrage
This skill alone can power a lead gen agency. Package + resell.

---

## Discovery Sources

| Source | Best For | Rate Limits | Setup |
|--------|----------|-------------|-------|
| X/Twitter | Tech, startup, crypto leads | 500/15min | API key |
| GitHub | Developer leads | 5000/hr | Token |
| Product Hunt | Startup founders | Scraping | None |
| Moltbook | AI/agent ecosystem | API | Key |
| LinkedIn* | B2B general | Via proxy | Careful |
| Custom RSS | Industry-specific | Varies | Config |

*LinkedIn requires careful handling. See `/discovery/linkedin-notes.md`

---

## Enrichment Stack

### Free Tier
- Email pattern guessing + verification
- Public social scraping
- Basic company data (website, description)
- Tech stack via BuiltWith (limited)

### Premium Tier (API costs)
- Hunter.io / Apollo.io integration
- Clearbit enrichment
- Full tech stack
- Funding data (Crunchbase)
- Intent signals

---

## Pricing (If Selling Leads)

| Lead Type | Enrichment Level | Market Rate |
|-----------|------------------|-------------|
| Basic (name + company) | None | $0.10-0.25 |
| Standard (+ email) | Email verified | $0.50-1.00 |
| Premium (+ phone, socials) | Full | $2-5 |
| Enterprise (+ intent + timing) | Full + signals | $5-15 |

---

## Requirements

- OpenClaw instance
- API keys for discovery sources
- Optional: enrichment provider API keys
- Storage for lead database

---

## Premium Version

Free version includes:
- 2 discovery sources (X + GitHub)
- Basic email pattern matching
- Simple ICP scoring
- JSON export

**Premium ($79) adds:**
- All discovery sources
- Full enrichment stack integration
- Advanced scoring algorithms
- CRM integrations (HubSpot, Pipedrive, etc.)
- Auto-outreach triggers
- Deduplication engine
- Lifetime updates

→ Get Premium: [link]

---

*Built for agents who sell.*

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
