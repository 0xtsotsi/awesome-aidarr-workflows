# kagi-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/silversteez/kagi-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/silversteez/kagi-search/SKILL.md)
> Category: Search & Research

---

## Description

Web search using Kagi Search API. Use when you need to search the web for current information, facts, or references. Requires KAGI_API_KEY in the environment.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Web search using Kagi Search API. Use when you need to search the web for current information, facts, or references. Requires KAGI_API_KEY in the environment.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run kagi-search`)
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
You are executing the kagi-search workflow. Use the following context:

Description: Web search using Kagi Search API. Use when you need to search the web for current information, facts, or references. Requires KAGI_API_KEY in the environment.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: kagi-search
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



> **Note:** The Kagi Search API is currently in beta. To request API access, email support@kagi.com. You must be a Kagi subscriber to use the API.
---

# Kagi Search CLI

Web search using the Kagi Search API with a clean, readable output format.

## Quick Start

```bash
export KAGI_API_KEY="your_api_key"
kagi-search "your search query"
# or run directly:
python3 scripts/kagi-search.py "your search query"
```

## Features

- **Clean output** - Title, URL, snippet, and metadata for each result
- **Pagination support** - Control result count and offset
- **JSON mode** - Raw JSON output for scripting
- **Related searches** - Shows related queries (can be hidden)
- **API balance** - Displays remaining API quota
- **Fast & lightweight** - Pure Python, no dependencies

## Options

| Flag | Description |
|------|-------------|
| `query` | Search terms (required) |
| `-n, --limit` | Number of results (default: 10) |
| `-s, --offset` | Offset for pagination (default: 0) |
| `--json` | Output raw JSON |
| `--no-related` | Hide related searches |
| `-h, --help` | Show help |

## Examples

```bash
# Basic search
kagi-search "python async await tutorial"

# Limit results
kagi-search "AI news" --limit 5

# Pagination
kagi-search "recipes" --offset 10 --limit 5

# JSON for scripting
kagi-search "github stars" --json | jq '.data[].url'

# Hide related searches
kagi-search "rust programming" --no-related
```

## Setup

**Environment:**
```bash
export KAGI_API_KEY="your_api_key"
# Add to ~/.bashrc or ~/.zshrc for persistence
```

**PATH access:**
```bash
# Make executable and add to PATH
chmod +x scripts/kagi-search.py
cp scripts/kagi-search.py ~/.local/bin/kagi-search
```

## Requirements

- Python 3.7+
- `KAGI_API_KEY` environment variable
- Internet connection

## Output Format

```
[Query: search terms]
[Results: 5]
[API Balance: $0.123]
[Time: 45ms]
----------------------------------------
=== Result Title ===
https://example.com
Snippet text here...
[2024-01-15]
---
Related: related query 1, related query 2
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
