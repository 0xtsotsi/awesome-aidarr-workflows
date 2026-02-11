# tts

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/amstko/tts/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/amstko/tts/SKILL.md)
> Category: Speech & Transcription

---

## Description

Convert text to speech using Hume AI (or OpenAI) API. Use when the user asks for an audio message, a voice reply, or to hear something "of vive voix".

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Convert text to speech using Hume AI (or OpenAI) API. Use when the user asks for an audio message, a voice reply, or to hear something "of vive voix".

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tts`)
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
You are executing the tts workflow. Use the following context:

Description: Convert text to speech using Hume AI (or OpenAI) API. Use when the user asks for an audio message, a voice reply, or to hear something "of vive voix".

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tts
category: Speech & Transcription
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Text-to-Speech (TTS)

Convert text to speech and generate audio files (MP3).

## Hume AI (Preferred)

- **Preferred Voice**: `9e1f9e4f-691a-4bb0-b87c-e306a4c838ef`
- **Keys**: Stored in environment as `HUME_API_KEY` and `HUME_SECRET_KEY`.

### Usage

```bash
HUME_API_KEY="..." HUME_SECRET_KEY="..." node {baseDir}/scripts/generate_hume_speech.js --text "Hello Jonathan" --output "output.mp3"
```

## OpenAI (Legacy)

- **Preferred Voice**: `nova`
- **Usage**: `OPENAI_API_KEY="..." node {baseDir}/scripts/generate_speech.js --text "..." --output "..."`

## General Notes

- The scripts print a `MEDIA:` line with the absolute path to the generated file.
- Use the `message` tool to send the resulting file to the user.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
