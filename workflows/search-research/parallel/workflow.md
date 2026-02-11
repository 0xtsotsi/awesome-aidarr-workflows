# parallel

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mvanhorn/parallel/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mvanhorn/parallel/SKILL.md)
> Category: Search & Research

---

## Description

High-accuracy web search and research via Parallel.ai API. Optimized for AI agents with rich excerpts and citations.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
High-accuracy web search and research via Parallel.ai API. Optimized for AI agents with rich excerpts and citations.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run parallel`)
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
You are executing the parallel workflow. Use the following context:

Description: High-accuracy web search and research via Parallel.ai API. Optimized for AI agents with rich excerpts and citations.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: parallel
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Parallel.ai 🔬

High-accuracy web search API built for AI agents. Outperforms Perplexity/Exa on research benchmarks.

## Setup

```bash
pip install parallel-web
```

API key is configured. Uses Python SDK.

```python
from parallel import Parallel
client = Parallel(api_key="YOUR_KEY")
response = client.beta.search(
    mode="one-shot",
    max_results=10,
    objective="your query"
)
```

## Quick Usage

```bash
# Search with Python SDK
python3 {baseDir}/scripts/search.py "Who is the CEO of Anthropic?" --max-results 5

# JSON output
python3 {baseDir}/scripts/search.py "latest AI news" --json
```

## Response Format

Returns structured results with:
- `search_id` - unique search identifier
- `results[]` - array of results with:
  - `url` - source URL
  - `title` - page title
  - `excerpts[]` - relevant text excerpts
  - `publish_date` - when available
- `usage` - API usage stats

## When to Use

- **Deep research** requiring cross-referenced facts
- **Company/person research** with citations
- **Fact-checking** with evidence-based outputs
- **Complex queries** that need multi-hop reasoning
- Higher accuracy than traditional search for research tasks

## API Reference

Docs: https://docs.parallel.ai
Platform: https://platform.parallel.ai

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
