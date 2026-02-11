# whisper-mlx-local

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/impkind/whisper-mlx-local/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/impkind/whisper-mlx-local/SKILL.md)
> Category: Speech & Transcription

---

## Description

Free local speech-to-text for Telegram and WhatsApp using MLX Whisper on Apple Silicon. Private, no API costs.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Free local speech-to-text for Telegram and WhatsApp using MLX Whisper on Apple Silicon. Private, no API costs.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run whisper-mlx-local`)
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
You are executing the whisper-mlx-local workflow. Use the following context:

Description: Free local speech-to-text for Telegram and WhatsApp using MLX Whisper on Apple Silicon. Private, no API costs.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: whisper-mlx-local
category: Speech & Transcription
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Local Whisper

**Transcribe voice messages for free on Telegram and WhatsApp.** No API keys. No costs. Runs on your Mac.

## The Problem

Voice transcription APIs cost money:
- OpenAI Whisper: **$0.006/minute**
- Groq: **$0.001/minute**  
- AssemblyAI: **$0.01/minute**

If you transcribe a lot of Telegram voice messages, it adds up.

## The Solution

This skill runs Whisper **locally on your Mac**. Same quality, **zero cost**.

- ✅ Free forever
- ✅ Private (audio never leaves your Mac)
- ✅ Fast (~1 second per message)
- ✅ Works offline

## ⚠️ Important Notes

- **First run downloads ~1.5GB model** — be patient, this only happens once
- **First transcription is slow** — model loads into memory (~10-30 seconds), then it's instant
- **Already using OpenAI API for transcription?** Replace your existing `tools.media.audio` config with the one below

## Quick Start

### 1. Install dependencies
```bash
pip3 install -r requirements.txt
```

### 2. Start the daemon
```bash
python3 scripts/daemon.py
```
First run will download the Whisper model (~1.5GB). Wait for "Ready" message.

### 3. Add to OpenClaw config

Add this to your `~/.openclaw/openclaw.json`:

```json
{
  "tools": {
    "media": {
      "audio": {
        "enabled": true,
        "models": [
          {
            "type": "cli",
            "command": "~/.openclaw/workspace/skills/local-whisper/scripts/transcribe.sh",
            "args": ["{{MediaPath}}"],
            "timeoutSeconds": 60
          }
        ]
      }
    }
  }
}
```

### 4. Restart gateway
```bash
openclaw gateway restart
```

Now voice messages from Telegram, WhatsApp, etc. will be transcribed locally for free!

### Manual test
```bash
./scripts/transcribe.sh voice_message.ogg
```

## Use Case: Telegram Voice Messages

Instead of paying for OpenAI API to transcribe incoming voice messages, point OpenClaw to this local daemon. Free transcription forever.

## Auto-Start on Login

```bash
cp com.local-whisper.plist ~/Library/LaunchAgents/
launchctl load ~/Library/LaunchAgents/com.local-whisper.plist
```

## API

Daemon runs at `localhost:8787`:

```bash
curl -X POST http://localhost:8787/transcribe -F "file=@audio.ogg"
# {"text": "Hello world", "language": "en"}
```

## Translation

Any language → English:

```bash
./scripts/transcribe.sh spanish_audio.ogg --translate
```

## Requirements

- macOS with Apple Silicon (M1/M2/M3/M4)
- Python 3.9+

## License

MIT

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
