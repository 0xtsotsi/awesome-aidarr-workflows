# sag

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/sag/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/sag/SKILL.md)
> Category: CLI Utilities

---

## Description

ElevenLabs text-to-speech with mac-style say UX.

**Homepage:** https://sag.sh
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
ElevenLabs text-to-speech with mac-style say UX.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run sag`)
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
You are executing the sag workflow. Use the following context:

Description: ElevenLabs text-to-speech with mac-style say UX.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: sag
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: https://sag.sh
```

---

## Original Skill Content



# sag

Use `sag` for ElevenLabs TTS with local playback.

API key (required)
- `ELEVENLABS_API_KEY` (preferred)
- `SAG_API_KEY` also supported by the CLI

Quick start
- `sag "Hello there"`
- `sag speak -v "Roger" "Hello"`
- `sag voices`
- `sag prompting` (model-specific tips)

Model notes
- Default: `eleven_v3` (expressive)
- Stable: `eleven_multilingual_v2`
- Fast: `eleven_flash_v2_5`

Pronunciation + delivery rules
- First fix: respell (e.g. "key-note"), add hyphens, adjust casing.
- Numbers/units/URLs: `--normalize auto` (or `off` if it harms names).
- Language bias: `--lang en|de|fr|...` to guide normalization.
- v3: SSML `<break>` not supported; use `[pause]`, `[short pause]`, `[long pause]`.
- v2/v2.5: SSML `<break time="1.5s" />` supported; `<phoneme>` not exposed in `sag`.

v3 audio tags (put at the entrance of a line)
- `[whispers]`, `[shouts]`, `[sings]`
- `[laughs]`, `[starts laughing]`, `[sighs]`, `[exhales]`
- `[sarcastic]`, `[curious]`, `[excited]`, `[crying]`, `[mischievously]`
- Example: `sag "[whispers] keep this quiet. [short pause] ok?"`

Voice defaults
- `ELEVENLABS_VOICE_ID` or `SAG_VOICE_ID`

Confirm voice + speaker before long output.

## Chat voice responses

When Peter asks for a "voice" reply (e.g., "crazy scientist voice", "explain in voice"), generate audio and send it:

```bash
# Generate audio file
sag -v Clawd -o /tmp/voice-reply.mp3 "Your message here"

# Then include in reply:
# MEDIA:/tmp/voice-reply.mp3
```

Voice character tips:
- Crazy scientist: Use `[excited]` tags, dramatic pauses `[short pause]`, vary intensity
- Calm: Use `[whispers]` or slower pacing
- Dramatic: Use `[sings]` or `[shouts]` sparingly

Default voice for Clawd: `lj2rcrvANS3gaWWnczSX` (or just `-v Clawd`)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
