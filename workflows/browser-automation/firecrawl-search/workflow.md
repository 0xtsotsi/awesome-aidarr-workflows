# firecrawl-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ashwingupy/firecrawl-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ashwingupy/firecrawl-search/SKILL.md)
> Category: Browser & Automation

---

## Description

Web search and scraping via Firecrawl API. Use when you need to search the web, scrape websites (including JS-heavy pages), crawl entire sites, or extract structured data from web pages. Requires FIRECRAWL_API_KEY environment variable.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Web search and scraping via Firecrawl API. Use when you need to search the web, scrape websites (including JS-heavy pages), crawl entire sites, or extract structured data from web pages. Requires FIRECRAWL_API_KEY environment variable.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run firecrawl-search`)
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
You are executing the firecrawl-search workflow. Use the following context:

Description: Web search and scraping via Firecrawl API. Use when you need to search the web, scrape websites (including JS-heavy pages), crawl entire sites, or extract structured data from web pages. Requires FIRECRAWL_API_KEY environment variable.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: firecrawl-search
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Firecrawl

Web search and scraping via Firecrawl API.

## Prerequisites

Set `FIRECRAWL_API_KEY` in your environment or `.env` file:
```bash
export FIRECRAWL_API_KEY=fc-xxxxxxxxxx
```

## Quick Start

### Search the web
```bash
firecrawl_search "your search query" --limit 10
```

### Scrape a single page
```bash
firecrawl_scrape "https://example.com"
```

### Crawl an entire site
```bash
firecrawl_crawl "https://example.com" --max-pages 50
```

## API Reference

See [references/api.md](references/api.md) for detailed API documentation and advanced options.

## Scripts

- `scripts/search.py` - Search the web with Firecrawl
- `scripts/scrape.py` - Scrape a single URL
- `scripts/crawl.py` - Crawl an entire website

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
