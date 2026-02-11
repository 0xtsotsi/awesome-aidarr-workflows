# voice-ai-tts

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/gizmogremlin/voice-ai-tts/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/gizmogremlin/voice-ai-tts/SKILL.md)
> Category: Speech & Transcription

---

## Description

High-quality voice synthesis with 9 personas, 11 languages, streaming, and voice cloning using Voice.ai API.


**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
High-quality voice synthesis with 9 personas, 11 languages, streaming, and voice cloning using Voice.ai API.


### O - Orchestration
**Trigger:** User-invocable (via `aidarr run voice-ai-tts`)
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
You are executing the voice-ai-tts workflow. Use the following context:

Description: High-quality voice synthesis with 9 personas, 11 languages, streaming, and voice cloning using Voice.ai API.


Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: voice-ai-tts
category: Speech & Transcription
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Voice.ai Voices

## ✨ Features

- **9 Voice Personas** - Carefully curated voices for different use cases
- **11 Languages** - Multi-language synthesis with multilingual model
- **Streaming Mode** - Real-time audio output as it generates
- **Voice Cloning** - Clone voices from audio samples
- **Voice Design** - Customize with temperature and top_p parameters
- **OpenClaw Integration** - Works with OpenClaw's built-in TTS

## 🎙️ Available Voices

| Voice   | Gender | Persona     | Best For                   |
|---------|--------|-------------|----------------------------|
| ellie   | female | youthful    | Vlogs, social content      |
| oliver  | male   | british     | Narration, tutorials       |
| lilith  | female | soft        | ASMR, calm content         |
| smooth  | male   | deep        | Documentaries, audiobooks  |
| corpse  | male   | distinctive | Gaming, entertainment      |
| skadi   | female | anime       | Character voices           |
| zhongli | male   | deep        | Gaming, dramatic content   |
| flora   | female | cheerful    | Kids content, upbeat       |
| chief   | male   | heroic      | Gaming, action content     |

## 🌍 Languages

Available: `en`, `es`, `fr`, `de`, `it`, `pt`, `pl`, `ru`, `nl`, `sv`, `ca`

## 🎨 Voice Design

Customize voice output with these parameters:

- **temperature** (0-2) — Higher = more expressive, lower = more consistent
- **top_p** (0-1) — Controls randomness in speech generation

## 📡 Streaming Mode

Generate audio with real-time streaming (good for long texts):

```bash
# Stream audio as it generates
node scripts/tts.js --text "This is a long story..." --voice ellie --stream

# Streaming with custom output
node scripts/tts.js --text "Chapter one..." --voice oliver --stream --output chapter1.mp3
```

## 🔗 OpenClaw TTS Integration

```yaml
tts:
  skill: voice-ai-tts
  voice_id: d1bf0f33-8e0e-4fbf-acf8-45c3c6262513
```

## 💬 Triggering TTS in Chat

```
/tts Hello, welcome to Voice.ai!
```

## 💻 CLI Usage

```bash
export VOICE_AI_API_KEY="your-api-key"

# Generate speech
node scripts/tts.js --text "Hello world!" --voice ellie

# Choose different voice
node scripts/tts.js --text "Good morning!" --voice oliver --output morning.mp3

# Show help
node scripts/tts.js --help
```

## 🔗 Links

- [Voice.ai Docs](https://voice.ai/docs)
- [API Reference](https://voice.ai/docs/api-reference/text-to-speech/generate-speech)


---

Made with ❤️ by [Nick Gill](https://github.com/gizmoGremlin)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
