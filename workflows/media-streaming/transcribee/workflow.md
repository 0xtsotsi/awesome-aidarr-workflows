# transcribee

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/itsfabioroma/transcribee/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/itsfabioroma/transcribee/SKILL.md)
> Category: Media & Streaming

---

## Description

Transcribe YouTube videos and local audio/video files with speaker diarization. Use when user asks to transcribe a YouTube URL, podcast, video, or audio file. Outputs clean speaker-labeled transcripts ready for LLM analysis.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Transcribe YouTube videos and local audio/video files with speaker diarization. Use when user asks to transcribe a YouTube URL, podcast, video, or audio file. Outputs clean speaker-labeled transcripts ready for LLM analysis.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run transcribee`)
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
You are executing the transcribee workflow. Use the following context:

Description: Transcribe YouTube videos and local audio/video files with speaker diarization. Use when user asks to transcribe a YouTube URL, podcast, video, or audio file. Outputs clean speaker-labeled transcripts ready for LLM analysis.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: transcribee
category: Media & Streaming
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Transcribee

Transcribe YouTube videos and local media files with speaker diarization via ElevenLabs.

## Usage

```bash
# YouTube video
transcribee "https://www.youtube.com/watch?v=..."

# Local video
transcribee ~/path/to/video.mp4

# Local audio
transcribee ~/path/to/podcast.mp3
```

**Always quote URLs** containing `&` or special characters.

## Output

Transcripts save to: `~/Documents/transcripts/{category}/{title}-{date}/`

| File | Use |
|------|-----|
| `transcription.txt` | Speaker-labeled transcript |
| `transcription-raw.txt` | Plain text, no speakers |
| `transcription-raw.json` | Word-level timings |
| `metadata.json` | Video info, language, category |

## Supported Formats

- **Audio:** mp3, m4a, wav, ogg, flac
- **Video:** mp4, mkv, webm, mov, avi
- **URLs:** youtube.com, youtu.be

## Dependencies

```bash
brew install yt-dlp ffmpeg
```

## Troubleshooting

| Error | Fix |
|-------|-----|
| `yt-dlp not found` | `brew install yt-dlp` |
| `ffmpeg not found` | `brew install ffmpeg` |
| API errors | Check `.env` file in transcribee directory |

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
