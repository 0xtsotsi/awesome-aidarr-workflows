# voice-transcribe

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/darinkishore/voice-transcribe/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/darinkishore/voice-transcribe/SKILL.md)
> Category: Speech & Transcription

---

## Description

Transcribe audio files using OpenAI's gpt-4o-mini-transcribe model with vocabulary hints and text replacements. Requires uv (https://docs.astral.sh/uv/).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Transcribe audio files using OpenAI's gpt-4o-mini-transcribe model with vocabulary hints and text replacements. Requires uv (https://docs.astral.sh/uv/).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run voice-transcribe`)
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
You are executing the voice-transcribe workflow. Use the following context:

Description: Transcribe audio files using OpenAI's gpt-4o-mini-transcribe model with vocabulary hints and text replacements. Requires uv (https://docs.astral.sh/uv/).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: voice-transcribe
category: Speech & Transcription
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# voice-transcribe

transcribe audio files using openai's gpt-4o-mini-transcribe model.

## when to use

when receiving voice memos (especially via whatsapp), just run:
```bash
uv run /Users/darin/clawd/skills/voice-transcribe/transcribe <audio-file>
```
then respond based on the transcribed content.

## fixing transcription errors

if darin says a word was transcribed wrong, add it to `vocab.txt` (for hints) or `replacements.txt` (for guaranteed fix). see sections below.

## supported formats

- mp3, mp4, mpeg, mpga, m4a, wav, webm, ogg, opus

## examples

```bash
# transcribe a voice memo
transcribe /tmp/voice-memo.ogg

# pipe to other tools
transcribe /tmp/memo.ogg | pbcopy
```

## setup

1. add your openai api key to `/Users/darin/clawd/skills/voice-transcribe/.env`:
   ```
   OPENAI_API_KEY=sk-...
   ```

## custom vocabulary

add words to `vocab.txt` (one per line) to help the model recognize names/jargon:
```
Clawdis
Clawdbot
```

## text replacements

if the model still gets something wrong, add a replacement to `replacements.txt`:
```
wrong spelling -> correct spelling
```

## notes

- assumes english (no language detection)
- uses gpt-4o-mini-transcribe model specifically
- caches by sha256 of audio file

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
