# mcp-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/simlocker/mcp-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/simlocker/mcp-skill/SKILL.md)
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
**Trigger:** User-invocable (via `aidarr run mcp-skill`)
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
You are executing the mcp-skill workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: mcp-skill
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# MCP Skill

This skill wraps the MCP at https://mcp.exa.ai/mcp for various tools such as web search, deep research, and more.

## Tools Included
- web_search_exa
- web_search_advanced_exa
- get_code_context_exa
- deep_search_exa
- crawling_exa
- company_research_exa
- linkedin_search_exa
- deep_researcher_start
- deep_researcher_check

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
