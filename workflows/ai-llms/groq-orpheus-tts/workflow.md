# groq-orpheus-tts

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/eid33552-maker/groq-orpheus-tts/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/eid33552-maker/groq-orpheus-tts/SKILL.md)
> Category: AI & LLMs

---

## Description

Fast and FREE Arabic (Saudi) & English AI voices. Generous 100 requests per day via Groq API. Professional, high-quality generative TTS using Orpheus models.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Fast and FREE Arabic (Saudi) & English AI voices. Generous 100 requests per day via Groq API. Professional, high-quality generative TTS using Orpheus models.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run groq-orpheus-tts`)
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
You are executing the groq-orpheus-tts workflow. Use the following context:

Description: Fast and FREE Arabic (Saudi) & English AI voices. Generous 100 requests per day via Groq API. Professional, high-quality generative TTS using Orpheus models.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: groq-orpheus-tts
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Groq Orpheus TTS

A powerful and fast text-to-speech skill that leverages Groq's Orpheus models. 

**Key Features:**
- **100% Free Tier Friendly:** Uses the Groq Free API key (100 requests per day).
- **Ultra-Fast:** Near-instant audio generation.
- **High Quality:** Professional generative AI voices.

**Supported Languages:**
- **Arabic:** Authentic Saudi dialect synthesis (Voices: `fahad`, `sultan`, `noura`, `lulwa`, `aisha`).
- **English:** Expressive, high-quality speech (Voices: `autumn`, `diana`, `hannah`, `austin`, `daniel`, `troy`).

## Requirements

- **API Key:** A `GROQ_API_KEY` from the [Groq Console](https://console.groq.com/keys). This is FREE.
- **Terms:** You must accept the model terms for `orpheus-v1-english` on the [Groq Playground](https://console.groq.com/playground?model=canopylabs%2Forpheus-v1-english) before using the English model.
- **Tools:** `ffmpeg` must be installed on your system for audio conversion.

## Requirements

- **API Key:** `GROQ_API_KEY` from [Groq Console](https://console.groq.com/keys).
- **Terms:** You must accept the model terms for `orpheus-v1-english` on the [Groq Playground](https://console.groq.com/playground?model=canopylabs%2Forpheus-v1-english) before using the English model.
- **Tools:** `ffmpeg` must be installed on your system for audio conversion.

## Usage

You can ask the assistant to say something or generate an audio file.

### Voices Available

- **Arabic (`ar`):** `fahad` (Male), `sultan` (Male), `noura` (Female), `lulwa` (Female), `aisha` (Female).
- **English (`en`):** `autumn`, `diana`, `hannah`, `austin`, `daniel`, `troy`.

### Commands

```bash
# General usage
./groq-tts.sh "Text" output.mp3 [voice] [lang]

# Examples
./groq-tts.sh "أهلا بك" welcome.mp3 fahad ar
./groq-tts.sh "Hello world" hello.mp3 troy en
```

## Chat Responses

When you want the assistant to reply in voice, use:
```bash
./groq-tts.sh "Your message" /tmp/reply.mp3 fahad ar
# Then include MEDIA:/tmp/reply.mp3 in the response.
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
