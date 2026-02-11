# searxng

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/abk234/searxng/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/abk234/searxng/SKILL.md)
> Category: Search & Research

---

## Description

Privacy-respecting metasearch using your local SearXNG instance. Search the web, images, news, and more without external API dependencies.

**Homepage:** https://searxng.org
**Repository:** N/A
**Version:** 1.0.1

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Privacy-respecting metasearch using your local SearXNG instance. Search the web, images, news, and more without external API dependencies.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run searxng`)
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
You are executing the searxng workflow. Use the following context:

Description: Privacy-respecting metasearch using your local SearXNG instance. Search the web, images, news, and more without external API dependencies.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: searxng
category: Search & Research
version: 1.0.1
user_invocable: True
homepage: https://searxng.org
```

---

## Original Skill Content



# SearXNG Search

Search the web using your local SearXNG instance - a privacy-respecting metasearch engine.

## Commands

### Web Search
```bash
uv run {baseDir}/scripts/searxng.py search "query"              # Top 10 results
uv run {baseDir}/scripts/searxng.py search "query" -n 20        # Top 20 results
uv run {baseDir}/scripts/searxng.py search "query" --format json # JSON output
```

### Category Search
```bash
uv run {baseDir}/scripts/searxng.py search "query" --category images
uv run {baseDir}/scripts/searxng.py search "query" --category news
uv run {baseDir}/scripts/searxng.py search "query" --category videos
```

### Advanced Options
```bash
uv run {baseDir}/scripts/searxng.py search "query" --language en
uv run {baseDir}/scripts/searxng.py search "query" --time-range day
```

## Configuration

**Required:** Set the `SEARXNG_URL` environment variable to your SearXNG instance:

```bash
export SEARXNG_URL=https://your-searxng-instance.com
```

Or configure in your Clawdbot config:
```json
{
  "env": {
    "SEARXNG_URL": "https://your-searxng-instance.com"
  }
}
```

Default (if not set): `http://localhost:8080`

## Features

- 🔒 Privacy-focused (uses your local instance)
- 🌐 Multi-engine aggregation
- 📰 Multiple search categories
- 🎨 Rich formatted output
- 🚀 Fast JSON mode for programmatic use

## API

Uses your local SearXNG JSON API endpoint (no authentication required by default).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
