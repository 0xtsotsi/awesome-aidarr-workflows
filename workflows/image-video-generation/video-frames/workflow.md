# video-frames

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/video-frames/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/video-frames/SKILL.md)
> Category: Image & Video Generation

---

## Description

Extract frames or short clips from videos using ffmpeg.

**Homepage:** https://ffmpeg.org
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Extract frames or short clips from videos using ffmpeg.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run video-frames`)
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
You are executing the video-frames workflow. Use the following context:

Description: Extract frames or short clips from videos using ffmpeg.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: video-frames
category: Image & Video Generation
version: 1.0.0
user_invocable: True
homepage: https://ffmpeg.org
```

---

## Original Skill Content



# Video Frames (ffmpeg)

Extract a single frame from a video, or create quick thumbnails for inspection.

## Quick start

First frame:

```bash
{baseDir}/scripts/frame.sh /path/to/video.mp4 --out /tmp/frame.jpg
```

At a timestamp:

```bash
{baseDir}/scripts/frame.sh /path/to/video.mp4 --time 00:00:10 --out /tmp/frame-10s.jpg
```

## Notes

- Prefer `--time` for “what is happening around here?”.
- Use a `.jpg` for quick share; use `.png` for crisp UI frames.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
