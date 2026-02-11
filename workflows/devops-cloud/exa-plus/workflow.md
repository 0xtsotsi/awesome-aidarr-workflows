# exa-plus

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jordyvandomselaar/exa-plus/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jordyvandomselaar/exa-plus/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Neural web search via Exa AI. Search people, companies, news, research, code. Supports deep search, domain filters, date ranges.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Neural web search via Exa AI. Search people, companies, news, research, code. Supports deep search, domain filters, date ranges.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run exa-plus`)
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
You are executing the exa-plus workflow. Use the following context:

Description: Neural web search via Exa AI. Search people, companies, news, research, code. Supports deep search, domain filters, date ranges.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: exa-plus
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Exa - Neural Web Search

Powerful AI-powered search with LinkedIn, news, research papers, and more.

## Setup

Create `~/.clawdbot/credentials/exa/config.json`:
```json
{"apiKey": "your-exa-api-key"}
```

## Commands

### General Search
```bash
bash scripts/search.sh "query" [options]
```

Options (as env vars):
- `NUM=10` - Number of results (max 100)
- `TYPE=auto` - Search type: auto, neural, fast, deep
- `CATEGORY=` - Category: news, company, people, research paper, github, tweet, pdf, financial report
- `DOMAINS=` - Include domains (comma-separated)
- `EXCLUDE=` - Exclude domains (comma-separated)
- `SINCE=` - Published after (ISO date)
- `UNTIL=` - Published before (ISO date)
- `LOCATION=NL` - User location (country code)

### Examples

```bash
# Basic search
bash scripts/search.sh "AI agents 2024"

# LinkedIn people search
CATEGORY=people bash scripts/search.sh "software engineer Amsterdam"

# Company search
CATEGORY=company bash scripts/search.sh "fintech startup Netherlands"

# News from specific domain
CATEGORY=news DOMAINS="reuters.com,bbc.com" bash scripts/search.sh "Netherlands"

# Research papers
CATEGORY="research paper" bash scripts/search.sh "transformer architecture"

# Deep search (comprehensive)
TYPE=deep bash scripts/search.sh "climate change solutions"

# Date-filtered news
CATEGORY=news SINCE="2026-01-01" bash scripts/search.sh "tech layoffs"
```

### Get Content
Extract full text from URLs:
```bash
bash scripts/content.sh "url1" "url2"
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
