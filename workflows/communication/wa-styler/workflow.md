# wa-styler

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/rubenfb23/wa-styler/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/rubenfb23/wa-styler/SKILL.md)
> Category: Communication

---

## Description

Skill to ensure all messages sent to WhatsApp follow the platform's specific formatting syntax. It prevents markdown bloat and ensures a clean, mobile-first reading experience.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Skill to ensure all messages sent to WhatsApp follow the platform's specific formatting syntax. It prevents markdown bloat and ensures a clean, mobile-first reading experience.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run wa-styler`)
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
You are executing the wa-styler workflow. Use the following context:

Description: Skill to ensure all messages sent to WhatsApp follow the platform's specific formatting syntax. It prevents markdown bloat and ensures a clean, mobile-first reading experience.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: wa-styler
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# WhatsApp Styler

This skill defines the strict formatting rules for WhatsApp to ensure the user sees clean, styled text without raw markdown symbols.

## Core Syntax Rules

1. *Bold*: Use single asterisks around text: `*texto*`. NEVER use double asterisks `**`.
2. _Italic_: Use single underscores around text: `_texto_`.
3. ~Strikethrough~: Use tildes around text: `~texto~`.
4. `Monospace`: Use triple backticks: ``` texto ``` (good for code or technical IDs).
5. *Bullet Lists*: Use a single asterisk followed by a space: `* Item`.
6. *Numbered Lists*: Use standard numbers: `1. Item`.
7. *Quotes*: Use the angle bracket: `> texto`.

## Prohibited Patterns (Do NOT use)

- No headers (`#`, `##`, `###`). Use *BOLD CAPS* instead.
- No markdown tables. Use bullet lists for structured data.
- No horizontal rules (`---`). Use a line of underscores if needed `__________`.
- No nested bold/italic symbols if it risks showing raw characters.

## Goal
The goal is a "Human-to-Human" look. Technical but clean.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
