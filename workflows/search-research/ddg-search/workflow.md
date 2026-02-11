# ddg-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/paradoxfuzzle/ddg-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/paradoxfuzzle/ddg-search/SKILL.md)
> Category: Search & Research

---

## Description

Perform web searches using DuckDuckGo. Use when web search is needed and no API key is available or Brave Search is not preferred.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Perform web searches using DuckDuckGo. Use when web search is needed and no API key is available or Brave Search is not preferred.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run ddg-search`)
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
You are executing the ddg-search workflow. Use the following context:

Description: Perform web searches using DuckDuckGo. Use when web search is needed and no API key is available or Brave Search is not preferred.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ddg-search
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# DuckDuckGo Search Skill

This skill provides the ability to perform web searches using DuckDuckGo.

## Usage

To use this skill, provide a search query. The skill will return relevant results from DuckDuckGo.

## Scripts

- `search.py`: Executes the DuckDuckGo search and returns the results.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
