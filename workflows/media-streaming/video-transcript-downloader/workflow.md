# video-transcript-downloader

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/video-transcript-downloader/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/video-transcript-downloader/SKILL.md)
> Category: Media & Streaming

---

## Description

Download videos, audio, subtitles, and clean paragraph-style transcripts from YouTube and any other yt-dlp supported site. Use when asked to “download this video”, “save this clip”, “rip audio”, “get subtitles”, “get transcript”, or to troubleshoot yt-dlp/ffmpeg and formats/playlists.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Download videos, audio, subtitles, and clean paragraph-style transcripts from YouTube and any other yt-dlp supported site. Use when asked to “download this video”, “save this clip”, “rip audio”, “get subtitles”, “get transcript”, or to troubleshoot yt-dlp/ffmpeg and formats/playlists.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run video-transcript-downloader`)
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
You are executing the video-transcript-downloader workflow. Use the following context:

Description: Download videos, audio, subtitles, and clean paragraph-style transcripts from YouTube and any other yt-dlp supported site. Use when asked to “download this video”, “save this clip”, “rip audio”, “get subtitles”, “get transcript”, or to troubleshoot yt-dlp/ffmpeg and formats/playlists.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: video-transcript-downloader
category: Media & Streaming
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Video Transcript Downloader

`./scripts/vtd.js` can:
- Print a transcript as a clean paragraph (timestamps optional).
- Download video/audio/subtitles.

Transcript behavior:
- YouTube: fetch via `youtube-transcript-plus` when possible.
- Otherwise: pull subtitles via `yt-dlp`, then clean into a paragraph.

## Setup

```bash
cd ~/Projects/agent-scripts/skills/video-transcript-downloader && npm ci
```

## Transcript (default: clean paragraph)

```bash
./scripts/vtd.js transcript --url 'https://…'
./scripts/vtd.js transcript --url 'https://…' --lang en
./scripts/vtd.js transcript --url 'https://…' --timestamps
./scripts/vtd.js transcript --url 'https://…' --keep-brackets
```

## Download video / audio / subtitles

```bash
./scripts/vtd.js download --url 'https://…' --output-dir ~/Downloads
./scripts/vtd.js audio --url 'https://…' --output-dir ~/Downloads
./scripts/vtd.js subs --url 'https://…' --output-dir ~/Downloads --lang en
```

## Formats (list + choose)

List available formats (format ids, resolution, container, audio-only, etc):

```bash
./scripts/vtd.js formats --url 'https://…'
```

Download a specific format id (example):

```bash
./scripts/vtd.js download --url 'https://…' --output-dir ~/Downloads -- --format 137+140
```

Prefer MP4 container without re-encoding (remux when possible):

```bash
./scripts/vtd.js download --url 'https://…' --output-dir ~/Downloads -- --remux-video mp4
```

## Notes

- Default transcript output is a single paragraph. Use `--timestamps` only when asked.
- Bracketed cues like `[Music]` are stripped by default; keep them via `--keep-brackets`.
- Pass extra `yt-dlp` args after `--` for `transcript` fallback, `download`, `audio`, `subs`, `formats`.

```bash
./scripts/vtd.js formats --url 'https://…' -- -v
```

## Troubleshooting (only when needed)

- Missing `yt-dlp` / `ffmpeg`:

```bash
brew install yt-dlp ffmpeg
```

- Verify:

```bash
yt-dlp --version
ffmpeg -version | head -n 1
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
