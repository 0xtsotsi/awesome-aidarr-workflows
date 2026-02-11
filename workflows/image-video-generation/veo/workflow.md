# veo

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/buddyh/veo/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/buddyh/veo/SKILL.md)
> Category: Image & Video Generation

---

## Description

Generate video using Google Veo (Veo 3.1 / Veo 3.0).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate video using Google Veo (Veo 3.1 / Veo 3.0).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run veo`)
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
You are executing the veo workflow. Use the following context:

Description: Generate video using Google Veo (Veo 3.1 / Veo 3.0).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: veo
category: Image & Video Generation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Veo (Google Video Generation)

Generate video clips using Google's Veo API.

Generate video
```bash
uv run {baseDir}/scripts/generate_video.py --prompt "your video description" --filename "output.mp4"
```

Options
- `--duration` / `-d`: Video duration in seconds (default: 8, max varies by model)
- `--aspect-ratio` / `-a`: Aspect ratio (16:9, 9:16, 1:1)
- `--model`: Veo model to use (veo-2.0-generate-001, veo-3.0-generate-001, veo-3.1-generate-preview, etc.)
- `--api-key`: Override GEMINI_API_KEY

API key
- `GEMINI_API_KEY` env var (preferred)
- Or set `skills."veo".env.GEMINI_API_KEY` in `~/.clawdbot/clawdbot.json`

Notes
- Veo 3.1 supports higher quality and longer durations
- Output is MP4 format
- Use `--model veo-3.1-generate-preview` for best results
- Veo 3.0-fast-generate-001 is faster but lower quality
- The script prints a `MEDIA:` line for Clawdbot to auto-attach on supported chat providers.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
