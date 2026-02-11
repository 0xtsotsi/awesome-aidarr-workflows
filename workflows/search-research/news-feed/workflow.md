# news-feed

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/lknik/news-feed/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/lknik/news-feed/SKILL.md)
> Category: Search & Research

---

## Description

Fetch latest news headlines from major RSS feeds (BBC, Reuters, AP, Al Jazeera, NPR, The Guardian, DW). No API keys required.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Fetch latest news headlines from major RSS feeds (BBC, Reuters, AP, Al Jazeera, NPR, The Guardian, DW). No API keys required.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run news-feed`)
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
You are executing the news-feed workflow. Use the following context:

Description: Fetch latest news headlines from major RSS feeds (BBC, Reuters, AP, Al Jazeera, NPR, The Guardian, DW). No API keys required.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: news-feed
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# News Feeds Skill

Fetch current news headlines and summaries from major international RSS feeds. Zero API keys, zero dependencies — uses only Python stdlib and HTTP.

## Available Commands

### Command: news
**What it does:** Fetch latest headlines from all configured feeds (or a specific source).
**How to execute:**
```bash
python3 {baseDir}/scripts/news.py
```

### Command: news from a specific source
**What it does:** Fetch headlines from one source only.
**How to execute:**
```bash
python3 {baseDir}/scripts/news.py --source bbc
python3 {baseDir}/scripts/news.py --source reuters
python3 {baseDir}/scripts/news.py --source ap
python3 {baseDir}/scripts/news.py --source guardian
python3 {baseDir}/scripts/news.py --source aljazeera
python3 {baseDir}/scripts/news.py --source npr
python3 {baseDir}/scripts/news.py --source dw
```

### Command: news by topic
**What it does:** Fetch headlines filtered to a specific topic/keyword.
```bash
python3 {baseDir}/scripts/news.py --topic "climate"
python3 {baseDir}/scripts/news.py --source bbc --topic "ukraine"
```

### Command: news with more items
**What it does:** Control how many items per feed (default 8).
```bash
python3 {baseDir}/scripts/news.py --limit 20
```

### Command: list sources
**What it does:** Show all available feed sources and their categories.
```bash
python3 {baseDir}/scripts/news.py --list-sources
```

## Available Sources

| Source       | Categories                                      |
|-------------|------------------------------------------------|
| bbc         | top, world, business, tech, science, health     |
| reuters      | top, world, business, tech, science, health     |
| ap          | top                                             |
| guardian    | top, world, business, tech, science             |
| aljazeera   | top                                             |
| npr         | top                                             |
| dw          | top                                             |

## When to Use

- User asks for latest news, current events, headlines
- User wants a news briefing or daily digest
- User asks "what's happening in the world"
- User asks about news on a specific topic
- User asks for a morning briefing

## Output Format

Returns markdown with headlines, short descriptions, publication times, and links. Grouped by source.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
