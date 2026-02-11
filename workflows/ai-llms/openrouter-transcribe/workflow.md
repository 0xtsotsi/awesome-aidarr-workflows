# openrouter-transcribe

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/obviyus/openrouter-transcribe/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/obviyus/openrouter-transcribe/SKILL.md)
> Category: AI & LLMs

---

## Description

Transcribe audio files via OpenRouter using audio-capable models (Gemini, GPT-4o-audio, etc).

**Homepage:** https://openrouter.ai/docs
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Transcribe audio files via OpenRouter using audio-capable models (Gemini, GPT-4o-audio, etc).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run openrouter-transcribe`)
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
You are executing the openrouter-transcribe workflow. Use the following context:

Description: Transcribe audio files via OpenRouter using audio-capable models (Gemini, GPT-4o-audio, etc).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openrouter-transcribe
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: https://openrouter.ai/docs
```

---

## Original Skill Content



# OpenRouter Audio Transcription

Transcribe audio files using OpenRouter's chat completions API with `input_audio` content type. Works with any audio-capable model.

## Quick start

```bash
{baseDir}/scripts/transcribe.sh /path/to/audio.m4a
```

Output goes to stdout.

## Useful flags

```bash
# Custom model (default: google/gemini-2.5-flash)
{baseDir}/scripts/transcribe.sh audio.ogg --model openai/gpt-4o-audio-preview

# Custom instructions
{baseDir}/scripts/transcribe.sh audio.m4a --prompt "Transcribe with speaker labels"

# Save to file
{baseDir}/scripts/transcribe.sh audio.m4a --out /tmp/transcript.txt

# Custom caller identifier (for OpenRouter dashboard)
{baseDir}/scripts/transcribe.sh audio.m4a --title "MyApp"
```

## How it works

1. Converts audio to WAV (mono, 16kHz) using ffmpeg
2. Base64 encodes the audio
3. Sends to OpenRouter chat completions with `input_audio` content
4. Extracts transcript from response

## API key

Set `OPENROUTER_API_KEY` env var, or configure in `~/.clawdbot/clawdbot.json`:

```json5
{
  skills: {
    "openrouter-transcribe": {
      apiKey: "YOUR_OPENROUTER_KEY"
    }
  }
}
```

## Headers

The script sends identification headers to OpenRouter:
- `X-Title`: Caller name (default: "Peanut/Clawdbot")
- `HTTP-Referer`: Reference URL (default: "https://clawdbot.com")

These show up in your OpenRouter dashboard for tracking.

## Troubleshooting

**ffmpeg format errors**: The script uses a temp directory (not `mktemp -t file.wav`) because macOS's mktemp adds random suffixes after the extension, breaking format detection.

**Argument list too long**: Large audio files produce huge base64 strings that exceed shell argument limits. The script writes to temp files (`--rawfile` for jq, `@file` for curl) instead of passing data as arguments.

**Empty response**: If you get "Empty response from API", the script will dump the raw response for debugging. Common causes:
- Invalid API key
- Model doesn't support audio input
- Audio file too large or corrupted

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
