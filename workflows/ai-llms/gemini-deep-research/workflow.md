# gemini-deep-research

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/arun-8687/gemini-deep-research/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/arun-8687/gemini-deep-research/SKILL.md)
> Category: AI & LLMs

---

## Description

Perform complex, long-running research tasks using Gemini Deep Research Agent. Use when asked to research topics requiring multi-source synthesis, competitive analysis, market research, or comprehensive technical investigations that benefit from systematic web search and analysis.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Perform complex, long-running research tasks using Gemini Deep Research Agent. Use when asked to research topics requiring multi-source synthesis, competitive analysis, market research, or comprehensive technical investigations that benefit from systematic web search and analysis.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run gemini-deep-research`)
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
You are executing the gemini-deep-research workflow. Use the following context:

Description: Perform complex, long-running research tasks using Gemini Deep Research Agent. Use when asked to research topics requiring multi-source synthesis, competitive analysis, market research, or comprehensive technical investigations that benefit from systematic web search and analysis.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: gemini-deep-research
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Gemini Deep Research

Use Gemini's Deep Research Agent to perform complex, long-running context gathering and synthesis tasks.

## Prerequisites

- `GEMINI_API_KEY` environment variable (from Google AI Studio)
- **Note**: This does NOT work with Antigravity OAuth tokens. Requires a direct Gemini API key.

## How It Works

Deep Research is an agent that:
1. Breaks down complex queries into sub-questions
2. Searches the web systematically
3. Synthesizes findings into comprehensive reports
4. Provides streaming progress updates

## Usage

### Basic Research

```bash
scripts/deep_research.py --query "Research the history of Google TPUs"
```

### Custom Output Format

```bash
scripts/deep_research.py --query "Research the competitive landscape of EV batteries" \
  --format "1. Executive Summary\n2. Key Players (include data table)\n3. Supply Chain Risks"
```

### With File Search (optional)

```bash
scripts/deep_research.py --query "Compare our 2025 fiscal year report against current public web news" \
  --file-search-store "fileSearchStores/my-store-name"
```

### Stream Progress

```bash
scripts/deep_research.py --query "Your research topic" --stream
```

## Output

The script saves results to timestamped files:
- `deep-research-YYYY-MM-DD-HH-MM-SS.md` - Final report in markdown
- `deep-research-YYYY-MM-DD-HH-MM-SS.json` - Full interaction metadata

## API Details

- **Endpoint**: `https://generativelanguage.googleapis.com/v1beta/interactions`
- **Agent**: `deep-research-pro-preview-12-2025`
- **Auth**: `x-goog-api-key` header (NOT OAuth Bearer token)

## Limitations

- Requires Gemini API key (get from [Google AI Studio](https://aistudio.google.com/apikey))
- Does NOT work with Antigravity OAuth authentication
- Long-running tasks (minutes to hours depending on complexity)
- May incur API costs depending on your quota

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
