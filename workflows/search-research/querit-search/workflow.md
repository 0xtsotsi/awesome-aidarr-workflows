# querit-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/interskh/querit-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/interskh/querit-search/SKILL.md)
> Category: Search & Research

---

## Description

Web search via Querit.ai API. Use when you need to search the web for documentation, current events, facts, or any web content. Returns structured results with titles, URLs, and snippets.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Web search via Querit.ai API. Use when you need to search the web for documentation, current events, facts, or any web content. Returns structured results with titles, URLs, and snippets.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run querit-search`)
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
You are executing the querit-search workflow. Use the following context:

Description: Web search via Querit.ai API. Use when you need to search the web for documentation, current events, facts, or any web content. Returns structured results with titles, URLs, and snippets.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: querit-search
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Querit Search

Web search and content extraction via the Querit.ai API. No browser required.

## Setup

Needs env: `QUERIT_API_KEY` — get a free key at https://querit.ai (1,000 queries/month).

## Search

```bash
node {baseDir}/search.js "query"                          # 5 results (default)
node {baseDir}/search.js "query" -n 10                    # more results (max 100)
node {baseDir}/search.js "query" --lang english            # language filter
node {baseDir}/search.js "query" --country "united states" # country filter
node {baseDir}/search.js "query" --date w1                 # past week (d1/w1/m1/y1)
node {baseDir}/search.js "query" --site-include github.com # only this domain
node {baseDir}/search.js "query" --site-exclude reddit.com # exclude domain
node {baseDir}/search.js "query" --content                 # also extract page content
node {baseDir}/search.js "query" --json                    # raw JSON output
```

Flags can be combined:

```bash
node {baseDir}/search.js "react hooks" -n 3 --lang english --site-include reactjs.org --content
```

## Extract Page Content

```bash
node {baseDir}/content.js https://example.com/article
```

Fetches a URL and extracts the main readable content as markdown.

## Output Format

### Search results (default)

```
1. Page Title
   https://example.com/page
   Site: example.com
   Age: 3 days ago
   Description snippet from search results

2. Another Page
   ...
```

### With --content

After the result listing, each page's extracted markdown content is appended:

```
### 1. Page Title
URL: https://example.com/page

# Extracted heading
Extracted body content in markdown...

---
```

### With --json

Raw JSON array of result objects with fields: `url`, `title`, `snippet`, `page_age`, `page_time`.

## When to Use

- Searching for documentation, API references, or tutorials
- Looking up facts, current events, or recent information
- Finding content from specific websites (use `--site-include`)
- Fetching and reading a web page's content (use `--content` or `content.js`)
- Any task requiring web search without interactive browsing

## Limitations

- Query limited to 72 characters (auto-truncated with warning)
- Max 100 results per query
- Max 20 domains per site filter
- Free tier: 1,000 queries/month, 1 QPS
- Supported languages: english, japanese, korean, german, french, spanish, portuguese

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
