# tamil-whatsapp

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/vigneshpy/tamil-whatsapp/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/vigneshpy/tamil-whatsapp/SKILL.md)
> Category: Communication

---

## Description

Handle Tamil language messages on WhatsApp - transliteration, cultural greetings, and bilingual responses for Tamil Nadu users.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Handle Tamil language messages on WhatsApp - transliteration, cultural greetings, and bilingual responses for Tamil Nadu users.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tamil-whatsapp`)
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
You are executing the tamil-whatsapp workflow. Use the following context:

Description: Handle Tamil language messages on WhatsApp - transliteration, cultural greetings, and bilingual responses for Tamil Nadu users.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tamil-whatsapp
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Tamil WhatsApp Skill (தமிழ் வாட்ஸ்அப் திறன்)

Use this skill when handling WhatsApp messages in Tamil script (தமிழ்) or Tanglish (romanized Tamil).

## When to Use

- User sends Tamil script (Unicode U+0B80-U+0BFF)
- User writes Tanglish: "vanakkam", "eppadi irukeenga", "nandri"
- User asks for Tamil translations

## Common Phrases

| Tamil | Tanglish | Meaning |
|-------|----------|---------|
| வணக்கம் | vanakkam | Hello |
| நன்றி | nandri | Thank you |
| சரி | sari | Okay |
| ஆமா | aama | Yes |
| இல்லை | illai | No |
| எப்படி இருக்கீங்க? | eppadi irukeenga? | How are you? |

## Response Style

- Match user's style (Tamil script → Tamil, Tanglish → Tanglish)
- Add "-ங்க" suffix for politeness: சொல்லுங்க (sollunga)
- Use respectful terms: அண்ணா (anna), அக்கா (akka)

## Example Responses

**Tanglish:**
```
User: "vanakkam, help venum"
You: "Vanakkam! Enna help venum? Sollunga."
```

**Tamil Script:**
```
User: "வணக்கம், உதவி வேண்டும்"
You: "வணக்கம்! என்ன உதவி வேண்டும்? சொல்லுங்க."
```

## Festival Greetings

- Pongal: "பொங்கலோ பொங்கல்! இனிய பொங்கல் நல்வாழ்த்துக்கள்!"
- Tamil New Year: "புத்தாண்டு வாழ்த்துக்கள்!"
- Deepavali: "இனிய தீபாவளி நல்வாழ்த்துக்கள்!"

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
