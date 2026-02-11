# spaces-listener

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jamesalmeida/spaces-listener/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jamesalmeida/spaces-listener/SKILL.md)
> Category: Marketing & Sales

---

## Description

Record, transcribe, and summarize X/Twitter Spaces — live or replays. Auto-downloads audio via yt-dlp, transcribes with Whisper, and generates AI summaries.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.6.0

**Tags:** twitter, x, spaces, transcription, summarization, audio, recording

---

## GOTCHA Framework

### G - Goals
Record, transcribe, and summarize X/Twitter Spaces — live or replays. Auto-downloads audio via yt-dlp, transcribes with Whisper, and generates AI summaries.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run spaces-listener`)
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
You are executing the spaces-listener workflow. Use the following context:

Description: Record, transcribe, and summarize X/Twitter Spaces — live or replays. Auto-downloads audio via yt-dlp, transcribes with Whisper, and generates AI summaries.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: spaces-listener
category: Marketing & Sales
version: 1.6.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# spaces-listener

Record, transcribe, and summarize X/Twitter Spaces — live or replays. Supports multiple concurrent recordings.

## Commands

```bash
# Start recording (runs in background)
spaces listen <url>

# Record multiple Spaces at once
spaces listen "https://x.com/i/spaces/1ABC..."
spaces listen "https://x.com/i/spaces/2DEF..."

# List all active recordings
spaces list

# Check specific recording status
spaces status 1

# Stop a recording
spaces stop 1
spaces stop all

# Clean stale pid/meta files
spaces clean

# Transcribe when done
spaces transcribe ~/Desktop/space.m4a --model medium

# Summarize an existing transcript
spaces summarize ~/Desktop/space_transcript.txt

# Skip summarization
spaces transcribe ~/Desktop/space.m4a --no-summarize
```

## Requirements

```bash
brew install yt-dlp ffmpeg openai-whisper
```

For summaries, set `OPENAI_API_KEY` (transcription still works without it).

## How It Works

1. Each `spaces listen` starts a new background recording with a unique ID
2. Recordings persist even if you close terminal
3. Run `spaces list` to see all active recordings
4. When done, `spaces stop <id>` or `spaces stop all`
5. Transcribe with `spaces transcribe <file>`
6. Summaries are generated automatically after transcription (skip with `--no-summarize`)

## Output

Each space gets its own folder under `~/Dropbox/ClawdBox/XSpaces/`:
```
~/Dropbox/ClawdBox/XSpaces/
  space_username_2026-02-03_1430/
    recording.m4a     — audio
    recording.log     — progress log
    transcript.txt    — transcript
    summary.txt       — summary
```

## Critical: Agent Usage Rules

**NEVER set a timeout on Space downloads.** Spaces can be hours long.
yt-dlp stops automatically when the Space ends — don't kill it early.

The correct workflow:
1. Run `spaces listen <url>` — it starts a background process and returns immediately
2. Set a **cron job** (every 5–10 min) to check `spaces list`
3. When recording shows "No active recordings", it's done
4. Transcribe the audio file, summarize, notify the user
5. Delete the cron job

**Do NOT:**
- Use `exec` with a timeout for downloads
- Run competing download processes for the same Space
- Kill the download process manually (unless the user asks)

Audio is staged in `/tmp/spaces-listener-staging/` during recording, then
automatically copied to the final Dropbox output dir when complete. This
avoids Dropbox file-locking issues during long downloads.

## Whisper Models

| Model | Speed | Accuracy |
|-------|-------|----------|
| tiny | ⚡⚡⚡⚡ | ⭐ |
| base | ⚡⚡⚡ | ⭐⭐ |
| small | ⚡⚡ | ⭐⭐⭐ |
| medium | ⚡ | ⭐⭐⭐⭐ |
| large | 🐢 | ⭐⭐⭐⭐⭐ |

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
