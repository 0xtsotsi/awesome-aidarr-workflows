# readwise

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/refrigerator/readwise/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/refrigerator/readwise/SKILL.md)
> Category: Notes & PKM

---

## Description

Access Readwise highlights and Reader saved articles

**Homepage:** https://readwise.io
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Access Readwise highlights and Reader saved articles

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run readwise`)
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
You are executing the readwise workflow. Use the following context:

Description: Access Readwise highlights and Reader saved articles

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: readwise
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: https://readwise.io
```

---

## Original Skill Content



# Readwise & Reader Skill

Access your Readwise highlights and Reader saved articles.

## Setup

Get your API token from: https://readwise.io/access_token

Set the environment variable:
```bash
export READWISE_TOKEN="your_token_here"
```

Or add to ~/.clawdbot/clawdbot.json under "env".

## Readwise (Highlights)

### List books/sources
```bash
node {baseDir}/scripts/readwise.mjs books [--limit 20]
```

### Get highlights from a book
```bash
node {baseDir}/scripts/readwise.mjs highlights [--book-id 123] [--limit 20]
```

### Search highlights
```bash
node {baseDir}/scripts/readwise.mjs search "query"
```

### Export all highlights (paginated)
```bash
node {baseDir}/scripts/readwise.mjs export [--updated-after 2024-01-01]
```

## Reader (Saved Articles)

### List documents
```bash
node {baseDir}/scripts/reader.mjs list [--location new|later|archive|feed] [--category article|book|podcast|...] [--limit 20]
```

### Get document details
```bash
node {baseDir}/scripts/reader.mjs get <document_id>
```

### Save a URL to Reader
```bash
node {baseDir}/scripts/reader.mjs save "https://example.com/article" [--location later]
```

### Search Reader
```bash
node {baseDir}/scripts/reader.mjs search "query"
```

## Notes
- Rate limits: 20 requests/minute for Readwise, varies for Reader
- All commands output JSON for easy parsing
- Use `--help` on any command for options

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
