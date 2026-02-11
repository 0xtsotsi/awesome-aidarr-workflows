# transcribe

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/javicasper/transcribe/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/javicasper/transcribe/SKILL.md)
> Category: Speech & Transcription

---

## Description

Transcribe audio files to text using local Whisper (Docker). Use when receiving voice messages, audio files (.mp3, .m4a, .ogg, .wav, .webm), or when asked to transcribe audio content.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Transcribe audio files to text using local Whisper (Docker). Use when receiving voice messages, audio files (.mp3, .m4a, .ogg, .wav, .webm), or when asked to transcribe audio content.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run transcribe`)
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
You are executing the transcribe workflow. Use the following context:

Description: Transcribe audio files to text using local Whisper (Docker). Use when receiving voice messages, audio files (.mp3, .m4a, .ogg, .wav, .webm), or when asked to transcribe audio content.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: transcribe
category: Speech & Transcription
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Transcribe

Local audio transcription using faster-whisper in Docker.

## Installation

```bash
cd /path/to/skills/transcribe/scripts
chmod +x install.sh
./install.sh
```

This builds the Docker image `whisper:local` and installs the `transcribe` CLI.

## Usage

```bash
transcribe /path/to/audio.mp3 [language]
```

- Default language: `es` (Spanish)
- Use `auto` for auto-detection
- Outputs plain text to stdout

## Examples

```bash
transcribe /tmp/voice.ogg          # Spanish (default)
transcribe /tmp/meeting.mp3 en     # English
transcribe /tmp/audio.m4a auto     # Auto-detect
```

## Supported Formats

mp3, m4a, ogg, wav, webm, flac, aac

## When Receiving Voice Messages

1. Save the audio attachment to a temp file
2. Run `transcribe <path>`
3. Include the transcription in your response
4. Clean up the temp file

## Files

- `scripts/transcribe` - CLI wrapper (bash)
- `scripts/install.sh` - Installation script (includes Dockerfile inline)

## Notes

- Model: `small` (fast) - edit install.sh for `large-v3` (accurate)
- Fully local, no API key needed

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
