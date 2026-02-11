# technews

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kesslerio/technews/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kesslerio/technews/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Fetches top stories from TechMeme, summarizes linked articles, and highlights social media reactions. Use when user wants tech news or says /technews.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Fetches top stories from TechMeme, summarizes linked articles, and highlights social media reactions. Use when user wants tech news or says /technews.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run technews`)
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
You are executing the technews workflow. Use the following context:

Description: Fetches top stories from TechMeme, summarizes linked articles, and highlights social media reactions. Use when user wants tech news or says /technews.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: technews
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# TechNews Skill

Fetches top stories from TechMeme, summarizes linked articles, and highlights social media buzz.

## Usage

**Command:** `/technews`

Fetches the top 10 stories from TechMeme, provides summaries from the linked articles, and highlights notable social media reactions.

## Setup

This skill requires:
- Python 3.9+
- `requests` and `beautifulsoup4` packages
- Optional: `tiktoken` for token-aware truncation

Install dependencies:
```bash
pip install requests beautifulsoup4
```

## Architecture

The skill works in three stages:

1. **Scrape TechMeme** — `scripts/techmeme_scraper.py` fetches and parses top stories
2. **Fetch Articles** — `scripts/article_fetcher.py` retrieves article content in parallel
3. **Summarize** — `scripts/summarizer.py` generates summaries and finds social reactions

## Commands

### /technews

Fetches and presents top tech news stories.

**Output includes:**
- Story title and original link
- AI-generated summary
- Social media highlights (Twitter reactions)
- Relevance score based on topic preferences

## How It Works

1. Scrapes TechMeme's homepage for top stories (by default, top 10)
2. For each story, fetches the linked article
3. Generates a concise summary (2-3 sentences)
4. Checks for notable social media reactions
5. Presents results in a clean, readable format

## State

- `<workspace>/memory/technews_history.json` — cache of recently fetched stories to avoid repeats

## Examples

- `/technews` — Get the latest tech news summary

## Future Expansion

This skill is designed to be extended to other sources:
- Hacker News (`/hn`)
- Reddit (`/reddit`)
- Other tech news aggregators

The modular architecture allows adding new source handlers without changing core functionality.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
