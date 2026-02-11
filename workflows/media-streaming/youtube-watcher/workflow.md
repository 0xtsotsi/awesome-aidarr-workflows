# youtube-watcher

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/michaelgathara/youtube-watcher/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/michaelgathara/youtube-watcher/SKILL.md)
> Category: Media & Streaming

---

## Description

Fetch and read transcripts from YouTube videos. Use when you need to summarize a video, answer questions about its content, or extract information from it.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Fetch and read transcripts from YouTube videos. Use when you need to summarize a video, answer questions about its content, or extract information from it.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run youtube-watcher`)
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
You are executing the youtube-watcher workflow. Use the following context:

Description: Fetch and read transcripts from YouTube videos. Use when you need to summarize a video, answer questions about its content, or extract information from it.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: youtube-watcher
category: Media & Streaming
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# YouTube Watcher

Fetch transcripts from YouTube videos to enable summarization, QA, and content extraction.

## Usage

### Get Transcript

Retrieve the text transcript of a video.

```bash
python3 {baseDir}/scripts/get_transcript.py "https://www.youtube.com/watch?v=VIDEO_ID"
```

## Examples

**Summarize a video:**

1. Get the transcript:
   ```bash
   python3 {baseDir}/scripts/get_transcript.py "https://www.youtube.com/watch?v=dQw4w9WgXcQ"
   ```
2. Read the output and summarize it for the user.

**Find specific information:**

1. Get the transcript.
2. Search the text for keywords or answer the user's question based on the content.

## Notes

- Requires `yt-dlp` to be installed and available in the PATH.
- Works with videos that have closed captions (CC) or auto-generated subtitles.
- If a video has no subtitles, the script will fail with an error message.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
