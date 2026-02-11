# openai-tts

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/pors/openai-tts/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/pors/openai-tts/SKILL.md)
> Category: AI & LLMs

---

## Description

Text-to-speech via OpenAI Audio Speech API.

**Homepage:** https://platform.openai.com/docs/guides/text-to-speech
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Text-to-speech via OpenAI Audio Speech API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run openai-tts`)
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
You are executing the openai-tts workflow. Use the following context:

Description: Text-to-speech via OpenAI Audio Speech API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openai-tts
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: https://platform.openai.com/docs/guides/text-to-speech
```

---

## Original Skill Content



# OpenAI TTS (curl)

Generate speech from text via OpenAI's `/v1/audio/speech` endpoint.

## Quick start

```bash
{baseDir}/scripts/speak.sh "Hello, world!"
{baseDir}/scripts/speak.sh "Hello, world!" --out /tmp/hello.mp3
```

Defaults:
- Model: `tts-1` (fast) or `tts-1-hd` (quality)
- Voice: `alloy` (neutral), also: `echo`, `fable`, `onyx`, `nova`, `shimmer`
- Format: `mp3`

## Voices

| Voice | Description |
|-------|-------------|
| alloy | Neutral, balanced |
| echo | Male, warm |
| fable | British, expressive |
| onyx | Deep, authoritative |
| nova | Female, friendly |
| shimmer | Female, soft |

## Flags

```bash
{baseDir}/scripts/speak.sh "Text" --voice nova --model tts-1-hd --out speech.mp3
{baseDir}/scripts/speak.sh "Text" --format opus --speed 1.2
```

Options:
- `--voice <name>`: alloy|echo|fable|onyx|nova|shimmer (default: alloy)
- `--model <name>`: tts-1|tts-1-hd (default: tts-1)
- `--format <fmt>`: mp3|opus|aac|flac|wav|pcm (default: mp3)
- `--speed <n>`: 0.25-4.0 (default: 1.0)
- `--out <path>`: output file (default: stdout or auto-named)

## API key

Set `OPENAI_API_KEY`, or configure in `~/.clawdbot/clawdbot.json`:

```json5
{
  skills: {
    entries: {
      "openai-tts": {
        apiKey: "sk-..."
      }
    }
  }
}
```

## Pricing

- tts-1: ~$0.015 per 1K characters
- tts-1-hd: ~$0.030 per 1K characters

Very affordable for short responses!

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
