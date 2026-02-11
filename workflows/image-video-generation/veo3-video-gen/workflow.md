# veo3-video-gen

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/bluelyw/veo3-video-gen/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/bluelyw/veo3-video-gen/SKILL.md)
> Category: Image & Video Generation

---

## Description

Generate and stitch short videos via Google Veo 3.x using the Gemini API (google-genai). Use when you need to create video clips from prompts (ads, UGC-style clips, product demos) and want a reproducible CLI workflow (generate, poll, download MP4, optionally stitch multiple segments).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate and stitch short videos via Google Veo 3.x using the Gemini API (google-genai). Use when you need to create video clips from prompts (ads, UGC-style clips, product demos) and want a reproducible CLI workflow (generate, poll, download MP4, optionally stitch multiple segments).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run veo3-video-gen`)
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
You are executing the veo3-video-gen workflow. Use the following context:

Description: Generate and stitch short videos via Google Veo 3.x using the Gemini API (google-genai). Use when you need to create video clips from prompts (ads, UGC-style clips, product demos) and want a reproducible CLI workflow (generate, poll, download MP4, optionally stitch multiple segments).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: veo3-video-gen
category: Image & Video Generation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Veo 3 Video Generation (Gemini API)

Use the bundled script to generate an MP4 from a text prompt.

## Generate (text → video)

```bash
uv run {baseDir}/scripts/generate_video.py \
  --prompt "A close up of ..." \
  --filename "out.mp4" \
  --model "veo-3.1-generate-preview" \
  --aspect-ratio "9:16" \
  --poll-seconds 10
```

## Generate a longer video by stitching segments

Veo commonly outputs ~8s clips per request. Use `--segments` to generate multiple clips and concatenate them with ffmpeg.

**Important:** This skill sends **one prompt per segment** (one Veo request per segment). Use `--base-style` to keep style consistent across segments.

```bash
uv run {baseDir}/scripts/generate_video.py \
  --prompt "Same scene, consistent style..." \
  --filename "out-24s.mp4" \
  --model "veo-3.1-generate-preview" \
  --aspect-ratio "9:16" \
  --segments 3 \
  --segment-style continuation
```

Options:
- `--base-style "..."`: prepended to every segment prompt (recommended).
- `--segment-prompt "..."` (repeatable): provide one prompt per segment (overrides `--prompt`).
- `--segment-style continuation` (default): appends continuity instructions per segment (only when using `--prompt`).
- `--segment-style same`: uses the exact same prompt for each segment (only when using `--prompt`).
- `--use-last-frame`: for segment >=2, extract previous segment last frame and pass it as `lastFrame` for continuity.
- `--emit-segment-media`: print `MEDIA:` for each segment as it finishes (useful for progress).
- `--keep-segments`: keep intermediate `*.segXX.mp4` files.
- `--reference-image path.jpg` (repeatable): guide generation with product/style references.

## Requirements

- `GEMINI_API_KEY` env var (or `--api-key`).
- `ffmpeg` on PATH when using `--segments > 1`.

## Troubleshooting

- 429/RESOURCE_EXHAUSTED: API key has no quota/billing for video.
- 503/UNAVAILABLE: model overloaded; retry later.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
