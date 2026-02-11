# youtube-transcript

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xthezealot/youtube-transcript/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xthezealot/youtube-transcript/SKILL.md)
> Category: Media & Streaming

---

## Description

Fetch and summarize YouTube video transcripts. Use when asked to summarize, transcribe, or extract content from YouTube videos. Handles transcript fetching via residential IP proxy to bypass YouTube's cloud IP blocks.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Fetch and summarize YouTube video transcripts. Use when asked to summarize, transcribe, or extract content from YouTube videos. Handles transcript fetching via residential IP proxy to bypass YouTube's cloud IP blocks.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run youtube-transcript`)
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
You are executing the youtube-transcript workflow. Use the following context:

Description: Fetch and summarize YouTube video transcripts. Use when asked to summarize, transcribe, or extract content from YouTube videos. Handles transcript fetching via residential IP proxy to bypass YouTube's cloud IP blocks.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: youtube-transcript
category: Media & Streaming
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# YouTube Transcript

Fetch transcripts from YouTube videos and optionally summarize them.

## Quick Start

```bash
python3 scripts/fetch_transcript.py <video_id_or_url> [languages]
```

**Examples:**
```bash
python3 scripts/fetch_transcript.py dQw4w9WgXcQ
python3 scripts/fetch_transcript.py "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
python3 scripts/fetch_transcript.py dQw4w9WgXcQ "fr,en,de"
```

**Output:** JSON with `video_id`, `title`, `author`, `full_text`, and timestamped `transcript` array.

## Workflow

1. Run `fetch_transcript.py` with video ID or URL
2. Script checks VPN, brings it up if needed
3. Returns JSON with full transcript text
4. Summarize the `full_text` field as needed

## Language Codes

Default priority: `en, fr, de, es, it, pt, nl`

Override with second argument: `python3 scripts/fetch_transcript.py VIDEO_ID "ja,ko,zh"`

## Setup & Configuration

See [references/SETUP.md](references/SETUP.md) for:
- Python dependencies installation
- WireGuard VPN configuration (required for cloud VPS)
- Troubleshooting common errors
- Alternative proxy options

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
