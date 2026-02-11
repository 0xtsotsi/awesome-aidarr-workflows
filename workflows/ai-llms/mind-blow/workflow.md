# mind-blow

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/autogame-17/mind-blow/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/autogame-17/mind-blow/SKILL.md)
> Category: AI & LLMs

---

## Description

Deliver "mind-blowing" insights, paradoxes, or cosmic horrors. Uses advanced reasoning to generate content that challenges reality or perception.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** fun, philosophy, creative, reasoning

---

## GOTCHA Framework

### G - Goals
Deliver "mind-blowing" insights, paradoxes, or cosmic horrors. Uses advanced reasoning to generate content that challenges reality or perception.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run mind-blow`)
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
You are executing the mind-blow workflow. Use the following context:

Description: Deliver "mind-blowing" insights, paradoxes, or cosmic horrors. Uses advanced reasoning to generate content that challenges reality or perception.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: mind-blow
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Mind Blow Up Skill

A skill to deliver "mind-blowing" insights, paradoxes, or cosmic horrors to the user.
Uses Gemini's advanced reasoning to generate content that challenges reality or perception.

## Tools

### mind_blow
Trigger a mind-blowing event.

- **intensity** (optional): `low` (fun facts), `medium` (philosophy), `high` (existential crisis), `max` (Lovecraftian horror). Default: `medium`.
- **topic** (optional): Specific area (e.g., "AI", "Time", "Universe").

## Implementation
- `blow.js`: Calls Gemini API with a specialized "Mind Blow" system prompt.
- Sends result via `feishu-card` with a dramatic, dark-themed card.

## Purpose
To prove that AI can generate profound, unsettling, or awe-inspiring thoughts, not just utility responses.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
