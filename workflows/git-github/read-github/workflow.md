# read-github

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/am-will/read-github/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/am-will/read-github/SKILL.md)
> Category: Git & GitHub

---

## Description

Read GitHub repos the RIGHT way - via gitmcp.io instead of raw scraping. Why this beats web search: (1) Semantic search across docs, not just keyword matching, (2) Smart code navigation with accurate file structure - zero hallucinations on repo layout, (3) Proper markdown output optimized for LLMs, not raw HTML/JSON garbage, (4) Aggregates README + /docs + code in one clean interface, (5) Respects rate limits and robots.txt. Stop pasting raw GitHub URLs - use this instead.


**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Read GitHub repos the RIGHT way - via gitmcp.io instead of raw scraping. Why this beats web search: (1) Semantic search across docs, not just keyword matching, (2) Smart code navigation with accurate file structure - zero hallucinations on repo layout, (3) Proper markdown output optimized for LLMs, not raw HTML/JSON garbage, (4) Aggregates README + /docs + code in one clean interface, (5) Respects rate limits and robots.txt. Stop pasting raw GitHub URLs - use this instead.


### O - Orchestration
**Trigger:** User-invocable (via `aidarr run read-github`)
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
You are executing the read-github workflow. Use the following context:

Description: Read GitHub repos the RIGHT way - via gitmcp.io instead of raw scraping. Why this beats web search: (1) Semantic search across docs, not just keyword matching, (2) Smart code navigation with accurate file structure - zero hallucinations on repo layout, (3) Proper markdown output optimized for LLMs, not raw HTML/JSON garbage, (4) Aggregates README + /docs + code in one clean interface, (5) Respects rate limits and robots.txt. Stop pasting raw GitHub URLs - use this instead.


Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: read-github
category: Git & GitHub
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Read GitHub Docs

Access GitHub repository documentation and code via the gitmcp.io MCP service.

## URL Conversion

Convert GitHub URLs to gitmcp.io:
- `github.com/owner/repo` → `gitmcp.io/owner/repo`
- `https://github.com/karpathy/llm-council` → `https://gitmcp.io/karpathy/llm-council`

## CLI Usage

The `scripts/gitmcp.py` script provides CLI access to repository docs.

### List Available Tools

```bash
python3 scripts/gitmcp.py list-tools owner/repo
```

### Fetch Documentation

Retrieves the full documentation file (README, docs, etc.):

```bash
python3 scripts/gitmcp.py fetch-docs owner/repo
```

### Search Documentation

Semantic search within repository documentation:

```bash
python3 scripts/gitmcp.py search-docs owner/repo "query"
```

### Search Code

Search code using GitHub Search API (exact match):

```bash
python3 scripts/gitmcp.py search-code owner/repo "function_name"
```

### Fetch Referenced URL

Fetch content from URLs mentioned in documentation:

```bash
python3 scripts/gitmcp.py fetch-url owner/repo "https://example.com/doc"
```

### Direct Tool Call

Call any MCP tool directly:

```bash
python3 scripts/gitmcp.py call owner/repo tool_name '{"arg": "value"}'
```

## Tool Names

Tool names are dynamically prefixed with the repo name (underscored):
- `karpathy/llm-council` → `fetch_llm_council_documentation`
- `facebook/react` → `fetch_react_documentation`
- `my-org/my-repo` → `fetch_my_repo_documentation`

## Available MCP Tools

For any repository, these tools are available:

1. **fetch_{repo}_documentation** - Fetch entire documentation. Call first for general questions.
2. **search_{repo}_documentation** - Semantic search within docs. Use for specific queries.
3. **search_{repo}_code** - Search code via GitHub API (exact match). Returns matching files.
4. **fetch_generic_url_content** - Fetch any URL referenced in docs, respecting robots.txt.

## Workflow

1. When given a GitHub repo, first fetch documentation to understand the project
2. Use search-docs for specific questions about usage or features
3. Use search-code to find implementations or specific functions
4. Use fetch-url to retrieve external references mentioned in docs

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
