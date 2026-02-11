# exa

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/fardeenxyz/exa/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/fardeenxyz/exa/SKILL.md)
> Category: Search & Research

---

## Description

Neural web search and code context via Exa AI API. Requires EXA_API_KEY. Use for finding documentation, code examples, research papers, or company info.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Neural web search and code context via Exa AI API. Requires EXA_API_KEY. Use for finding documentation, code examples, research papers, or company info.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run exa`)
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
You are executing the exa workflow. Use the following context:

Description: Neural web search and code context via Exa AI API. Requires EXA_API_KEY. Use for finding documentation, code examples, research papers, or company info.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: exa
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Exa - Neural Web Search

Direct API access to Exa's neural search engine.

## Setup

**1. Get your API Key:**
Get a key from [Exa Dashboard](https://dashboard.exa.ai/api-keys).

**2. Set it in your environment:**
```bash
export EXA_API_KEY="your-key-here"
```

## Usage

### Web Search
```bash
bash scripts/search.sh "query" [num_results] [type]
```
*   `type`: auto (default), neural, fast, deep
*   `category`: company, research-paper, news, github, tweet, personal-site, pdf

### Code Context
Finds relevant code snippets and documentation.
```bash
bash scripts/code.sh "query" [num_results]
```

### Get Content
Extract full text from URLs.
```bash
bash scripts/content.sh "url1" "url2"
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
