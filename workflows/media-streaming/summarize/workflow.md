# summarize

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/summarize/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/summarize/SKILL.md)
> Category: Media & Streaming

---

## Description

Summarize URLs or files with the summarize CLI (web, PDFs, images, audio, YouTube).

**Homepage:** https://summarize.sh
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Summarize URLs or files with the summarize CLI (web, PDFs, images, audio, YouTube).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run summarize`)
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
You are executing the summarize workflow. Use the following context:

Description: Summarize URLs or files with the summarize CLI (web, PDFs, images, audio, YouTube).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: summarize
category: Media & Streaming
version: 1.0.0
user_invocable: True
homepage: https://summarize.sh
```

---

## Original Skill Content



# Summarize

Fast CLI to summarize URLs, local files, and YouTube links.

## Quick start

```bash
summarize "https://example.com" --model google/gemini-3-flash-preview
summarize "/path/to/file.pdf" --model google/gemini-3-flash-preview
summarize "https://youtu.be/dQw4w9WgXcQ" --youtube auto
```

## Model + keys

Set the API key for your chosen provider:
- OpenAI: `OPENAI_API_KEY`
- Anthropic: `ANTHROPIC_API_KEY`
- xAI: `XAI_API_KEY`
- Google: `GEMINI_API_KEY` (aliases: `GOOGLE_GENERATIVE_AI_API_KEY`, `GOOGLE_API_KEY`)

Default model is `google/gemini-3-flash-preview` if none is set.

## Useful flags

- `--length short|medium|long|xl|xxl|<chars>`
- `--max-output-tokens <count>`
- `--extract-only` (URLs only)
- `--json` (machine readable)
- `--firecrawl auto|off|always` (fallback extraction)
- `--youtube auto` (Apify fallback if `APIFY_API_TOKEN` set)

## Config

Optional config file: `~/.summarize/config.json`

```json
{ "model": "openai/gpt-5.2" }
```

Optional services:
- `FIRECRAWL_API_KEY` for blocked sites
- `APIFY_API_TOKEN` for YouTube fallback

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
