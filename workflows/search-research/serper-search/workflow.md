# serper-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/samoppakiks/serper-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/samoppakiks/serper-search/SKILL.md)
> Category: Search & Research

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run serper-search`)
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
You are executing the serper-search workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: serper-search
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Serper Google Search Plugin

Native Clawdbot plugin for Google Search via [Serper.dev](https://serper.dev) API. Returns real Google results — organic links, knowledge graph, news, and "People Also Ask" — as a single tool call.

## When to use

- You need **actual Google results** with links and snippets (not AI-synthesized answers)
- You want Google News articles on a topic
- You need knowledge graph data (quick facts, entity info)
- Complements AI search tools (Perplexity, Brave) with raw Google data

## Setup

1. Get a free API key at [serper.dev](https://serper.dev) (2,500 searches/month, no card required)
2. Set the environment variable in your Clawdbot config:

```json
{
  "env": {
    "vars": {
      "SERPER_API_KEY": "your-api-key-here"
    }
  }
}
```

Or configure directly in the plugin entry:

```json
{
  "plugins": {
    "entries": {
      "serper-search": {
        "enabled": true,
        "config": {
          "apiKey": "your-api-key-here",
          "defaultNumResults": 5
        }
      }
    }
  }
}
```

## Usage

The plugin registers a `serper_search` tool with three parameters:

| Parameter | Type | Default | Description |
|-----------|------|---------|-------------|
| `query` | string | required | The search query |
| `num` | number | 5 | Number of results (1-100) |
| `searchType` | string | "search" | `"search"` for web, `"news"` for news |

### Web search

> Search for "best rust web frameworks 2026"

Returns organic results with title, link, snippet, and position, plus knowledge graph and related questions.

### News search

> Search news for "AI regulation Europe"

Returns news articles with title, link, snippet, date, and source.

## Plugin structure

```
serper-search/
  clawdbot.plugin.json   # Plugin manifest with configSchema
  package.json            # NPM package config
  index.ts                # Plugin implementation
  SKILL.md                # This file
```

## Key implementation details

- **Export**: `export default function register(api)` — not an object
- **Tool registration**: `api.registerTool(toolObject)` — direct, not callback
- **Return format**: `{ content: [{ type: "text", text: JSON.stringify(results) }] }`
- **Dependencies**: Symlink `@sinclair/typebox` from Clawdbot's own node_modules

## Author

Built by [@Samoppakiks](https://github.com/Samoppakiks) with Claude Code.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
