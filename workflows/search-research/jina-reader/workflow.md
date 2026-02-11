# jina-reader

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ericsantos/jina-reader/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ericsantos/jina-reader/SKILL.md)
> Category: Search & Research

---

## Description

Web content extraction via Jina AI Reader API. Three modes: read (URL to markdown), search (web search + full content), ground (fact-checking). Extracts clean content without exposing server IP.

**Homepage:** https://jina.ai/reader
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Web content extraction via Jina AI Reader API. Three modes: read (URL to markdown), search (web search + full content), ground (fact-checking). Extracts clean content without exposing server IP.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run jina-reader`)
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
You are executing the jina-reader workflow. Use the following context:

Description: Web content extraction via Jina AI Reader API. Three modes: read (URL to markdown), search (web search + full content), ground (fact-checking). Extracts clean content without exposing server IP.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: jina-reader
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: https://jina.ai/reader
```

---

## Original Skill Content



# Jina Reader

Extract clean web content via Jina AI — without exposing your server IP.

## Read a URL

```bash
{baseDir}/scripts/reader.sh "https://example.com/article"
```

## Search the web (top 5 results with full content)

```bash
{baseDir}/scripts/reader.sh --mode search "latest AI news 2025"
```

## Fact-check a statement

```bash
{baseDir}/scripts/reader.sh --mode ground "OpenAI was founded in 2015"
```

## Options

| Flag | Description | Default |
|------|-------------|---------|
| `--mode` | `read`, `search`, `ground` | `read` |
| `--selector` | CSS selector to extract specific region | — |
| `--wait` | CSS selector to wait for before extraction | — |
| `--remove` | CSS selectors to remove (comma-separated) | — |
| `--proxy` | Country code for geo-proxy (`br`, `us`, etc.) | — |
| `--nocache` | Force fresh content (skip cache) | off |
| `--format` | `markdown`, `html`, `text`, `screenshot` | `markdown` |
| `--json` | Raw JSON output | off |

## Examples

```bash
# Extract article content
{baseDir}/scripts/reader.sh "https://blog.example.com/post"

# Extract specific section via CSS selector
{baseDir}/scripts/reader.sh --selector "article.main" "https://example.com"

# Remove nav and ads before extraction
{baseDir}/scripts/reader.sh --remove "nav,footer,.ads" "https://example.com"

# Search with JSON output
{baseDir}/scripts/reader.sh --mode search --json "AI enterprise trends"

# Read via Brazil proxy
{baseDir}/scripts/reader.sh --proxy br "https://example.com.br"

# Fact-check a claim
{baseDir}/scripts/reader.sh --mode ground "Tesla is the most valuable car company"
```

## API Key

```bash
export JINA_API_KEY="jina_..."
```

Free tier: 10M tokens (no signup needed). Get key at https://jina.ai/reader/

## Pricing

- **Read:** ~$0.005/page (standard) | 3x for ReaderLM-v2
- **Search:** 10K tokens fixed + variable per result
- **Ground:** ~300K tokens/request (~30s latency)

## Why Jina Reader?

- **IP protection** — requests route through Jina's infra, not your server
- **Clean markdown** — readability extraction + optional ReaderLM-v2
- **Dynamic content** — headless Chrome renders JavaScript
- **Structured extraction** — JSON schema support for data extraction

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
