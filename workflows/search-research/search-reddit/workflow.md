# search-reddit

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/arkaydeus/search-reddit/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/arkaydeus/search-reddit/SKILL.md)
> Category: Search & Research

---

## Description

Search Reddit in real time using OpenAI web_search with enrichment (engagement + top comments). Use when you need recent Reddit threads, subreddit-filtered results, or quick link lists.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search Reddit in real time using OpenAI web_search with enrichment (engagement + top comments). Use when you need recent Reddit threads, subreddit-filtered results, or quick link lists.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run search-reddit`)
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
You are executing the search-reddit workflow. Use the following context:

Description: Search Reddit in real time using OpenAI web_search with enrichment (engagement + top comments). Use when you need recent Reddit threads, subreddit-filtered results, or quick link lists.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: search-reddit
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Search Reddit

Real-time Reddit search powered by OpenAI web_search with post enrichment (score, comments, and top comment excerpts).

## Setup

Set your OpenAI API key:

```bash
clawdbot config set skills.entries.search-reddit.apiKey "sk-YOUR-KEY"
```

Or use environment variable:
```bash
export OPENAI_API_KEY="sk-YOUR-KEY"
```

You can also set a shared key:
```bash
clawdbot config set skills.entries.openai.apiKey "sk-YOUR-KEY"
```

## Commands

### Basic Search
```bash
node {baseDir}/scripts/search.js "Claude Code tips"
```

### Filter by Time
```bash
node {baseDir}/scripts/search.js --days 7 "AI news"
```

### Filter by Subreddit
```bash
node {baseDir}/scripts/search.js --subreddits machinelearning,openai "agents"
node {baseDir}/scripts/search.js --exclude bots "real discussions"
```

### Output Options
```bash
node {baseDir}/scripts/search.js --json "topic"        # JSON results
node {baseDir}/scripts/search.js --compact "topic"     # Minimal output
node {baseDir}/scripts/search.js --links-only "topic"  # Only Reddit links
```

## Example Usage in Chat

**User:** "Search Reddit for what people are saying about Claude Code"
**Action:** Run search with query "Claude Code"

**User:** "Find posts in r/OpenAI from the last week"
**Action:** Run search with --subreddits openai --days 7

**User:** "Get Reddit links about Kimi K2.5"
**Action:** Run search with --links-only "Kimi K2.5"

## How It Works

Uses OpenAI Responses API (`/v1/responses`) with the `web_search` tool:
- Allowed domain: `reddit.com`
- Enriches each thread by fetching Reddit JSON (`/r/.../comments/.../.json`)
- Updates the date from `created_utc` and filters to last N days
- Computes engagement and top comment excerpts

## Environment Variables

- `OPENAI_API_KEY` - OpenAI API key (required)
- `SEARCH_REDDIT_MODEL` - Model override (default: gpt-5.2)
- `SEARCH_REDDIT_DAYS` - Default days to search (default: 30)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
