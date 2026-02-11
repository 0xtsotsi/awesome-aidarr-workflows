# gemini-yt-transcript

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/odrobnik/gemini-yt-video-transcript/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/odrobnik/gemini-yt-video-transcript/SKILL.md)
> Category: Search & Research

---

## Description

Create a verbatim transcript for a YouTube URL using Google Gemini (speaker labels, paragraph breaks; no time codes). Use when the user asks to transcribe a YouTube video or wants a clean transcript (no timestamps).

**Homepage:** https://github.com/odrobnik/gemini-yt-video-transcript-skill
**Repository:** N/A
**Version:** 1.0.2

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Create a verbatim transcript for a YouTube URL using Google Gemini (speaker labels, paragraph breaks; no time codes). Use when the user asks to transcribe a YouTube video or wants a clean transcript (no timestamps).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run gemini-yt-transcript`)
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
You are executing the gemini-yt-transcript workflow. Use the following context:

Description: Create a verbatim transcript for a YouTube URL using Google Gemini (speaker labels, paragraph breaks; no time codes). Use when the user asks to transcribe a YouTube video or wants a clean transcript (no timestamps).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: gemini-yt-transcript
category: Search & Research
version: 1.0.2
user_invocable: True
homepage: https://github.com/odrobnik/gemini-yt-video-transcript-skill
```

---

## Original Skill Content



# Gemini YouTube Video Transcript

Create a **verbatim transcript** for a YouTube URL using **Google Gemini**.

**Output format**
- First line: YouTube video title
- Then transcript lines only in the form:

```
Speaker: text
```

**Requirements**
- No time codes
- No extra headings / lists / commentary

## Usage

```bash
python3 {baseDir}/scripts/youtube_transcript.py "https://www.youtube.com/watch?v=..."
```

Options:
- `--out <path>` Write transcript to a specific file (default: auto-named in the workspace `out/` folder).

## Delivery

When chatting: send the resulting transcript as a document/attachment.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
