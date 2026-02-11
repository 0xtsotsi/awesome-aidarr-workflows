# songsee

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/songsee/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/songsee/SKILL.md)
> Category: CLI Utilities

---

## Description

Generate spectrograms and feature-panel visualizations from audio with the songsee CLI.

**Homepage:** https://github.com/steipete/songsee
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate spectrograms and feature-panel visualizations from audio with the songsee CLI.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run songsee`)
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
You are executing the songsee workflow. Use the following context:

Description: Generate spectrograms and feature-panel visualizations from audio with the songsee CLI.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: songsee
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: https://github.com/steipete/songsee
```

---

## Original Skill Content



# songsee

Generate spectrograms + feature panels from audio.

Quick start
- Spectrogram: `songsee track.mp3`
- Multi-panel: `songsee track.mp3 --viz spectrogram,mel,chroma,hpss,selfsim,loudness,tempogram,mfcc,flux`
- Time slice: `songsee track.mp3 --start 12.5 --duration 8 -o slice.jpg`
- Stdin: `cat track.mp3 | songsee - --format png -o out.png`

Common flags
- `--viz` list (repeatable or comma-separated)
- `--style` palette (classic, magma, inferno, viridis, gray)
- `--width` / `--height` output size
- `--window` / `--hop` FFT settings
- `--min-freq` / `--max-freq` frequency range
- `--start` / `--duration` time slice
- `--format` jpg|png

Notes
- WAV/MP3 decode native; other formats use ffmpeg if available.
- Multiple `--viz` renders a grid.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
