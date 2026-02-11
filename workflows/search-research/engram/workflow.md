# engram

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/anwitch/engram/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/anwitch/engram/SKILL.md)
> Category: Search & Research

---

## Description

Provides semantic search for a local knowledge base using Pinecone and Gemini embeddings.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Provides semantic search for a local knowledge base using Pinecone and Gemini embeddings.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run engram`)
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
You are executing the engram workflow. Use the following context:

Description: Provides semantic search for a local knowledge base using Pinecone and Gemini embeddings.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: engram
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# 🧠 Engram - Semantic Search Skill

This skill enables an AI agent to perform semantic searches on a local folder of Markdown files (e.g., an Obsidian vault). It finds information based on the meaning and context of a query, not just exact keywords.

## Tools

### engram_search

Searches the indexed knowledge base.

-   **`query`** (string, required): The natural language question to ask.
-   **`top_k`** (number, optional): The number of results to return.
-   **`min_score`** (number, optional): The minimum relevance score (0.0 to 1.0) for results.

### engram_index

Builds or updates the search index from the local Markdown files. This tool should be run periodically to keep the search memory synchronized.

## Author

-   **Andrie Wijaya** ([@Anwitch](https://github.com/Anwitch))

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
