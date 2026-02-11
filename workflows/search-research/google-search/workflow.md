# google-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mxfeinberg/google-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mxfeinberg/google-search/SKILL.md)
> Category: Search & Research

---

## Description

Search the web using Google Custom Search Engine (PSE). Use this when you need live information, documentation, or to research topics and the built-in web_search is unavailable.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search the web using Google Custom Search Engine (PSE). Use this when you need live information, documentation, or to research topics and the built-in web_search is unavailable.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run google-search`)
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
You are executing the google-search workflow. Use the following context:

Description: Search the web using Google Custom Search Engine (PSE). Use this when you need live information, documentation, or to research topics and the built-in web_search is unavailable.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: google-search
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Google Search Skill

This skill allows OpenClaw agents to perform web searches via Google's Custom Search API (PSE).

## Setup

1.  **Google Cloud Console:** Create a project and enable the "Custom Search API".
2.  **API Key:** Generate an API Key.
3.  **Search Engine ID (CX):** Create a Programmable Search Engine at [cse.google.com](https://cse.google.com/cse/all), and get your CX ID.
4.  **Environment:** Store your credentials in a `.env` file in your workspace:
    ```
    GOOGLE_API_KEY=your_key_here
    GOOGLE_CSE_ID=your_cx_id_here
    ```

## Workflow
... (rest of file)

## Example Usage

```bash
GOOGLE_API_KEY=xxx GOOGLE_CSE_ID=yyy python3 skills/google-search/scripts/search.py "OpenClaw documentation"
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
