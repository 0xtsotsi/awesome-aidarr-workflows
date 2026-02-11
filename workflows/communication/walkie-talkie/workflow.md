# walkie-talkie

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/rubenfb23/walkie-talkie/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/rubenfb23/walkie-talkie/SKILL.md)
> Category: Communication

---

## Description

Handles voice-to-voice conversations on WhatsApp. Automatically transcribes incoming audio and responds with local TTS audio. Use when the user wants to "talk" instead of type.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Handles voice-to-voice conversations on WhatsApp. Automatically transcribes incoming audio and responds with local TTS audio. Use when the user wants to "talk" instead of type.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run walkie-talkie`)
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
You are executing the walkie-talkie workflow. Use the following context:

Description: Handles voice-to-voice conversations on WhatsApp. Automatically transcribes incoming audio and responds with local TTS audio. Use when the user wants to "talk" instead of type.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: walkie-talkie
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Walkie-Talkie Mode

This skill automates the voice-to-voice loop on WhatsApp using local transcription and local TTS.

## Workflow

1. **Incoming Audio**: When a user sends an audio/ogg/opus file:
   - Use `tools/transcribe_voice.sh` to get the text.
   - Process the text as a normal user prompt.

2. **Outgoing Response**:
   - Instead of a text reply, generate speech using `bin/sherpa-onnx-tts`.
   - Send the resulting `.ogg` file back to the user as a voice note.

## Triggers

- User sends an audio message.
- User says "activa modo walkie-talkie" or "hablemos por voz".

## Constraints

- Use local tools only (ffmpeg, whisper-cpp, sherpa-onnx-tts).
- Maintain a fast response time (RTF < 0.5).
- Always reply with BOTH text (for clarity) and audio.

## Manual Execution (Internal)

To respond with voice manually:
```bash
bin/sherpa-onnx-tts /tmp/reply.ogg "Tu mensaje aquí"
```
Then send `/tmp/reply.ogg` via `message` tool with `filePath`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
