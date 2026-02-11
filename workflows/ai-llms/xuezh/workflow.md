# xuezh

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/local/xuezh/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/local/xuezh/SKILL.md)
> Category: AI & LLMs

---

## Description

Teach Mandarin using the xuezh engine for review, speaking, and audits.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Teach Mandarin using the xuezh engine for review, speaking, and audits.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run xuezh`)
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
You are executing the xuezh workflow. Use the following context:

Description: Teach Mandarin using the xuezh engine for review, speaking, and audits.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: xuezh
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Xuezh Skill

## Contract

Use the xuezh CLI exactly as specified. If a command is missing, ask for implementation instead of guessing.

## Default loop

1) Call `xuezh snapshot`.
2) Pick a tiny plan (1-2 bullets).
3) Run a short activity.
4) Log outcomes.

## CLI examples

```bash
xuezh snapshot --profile default
xuezh review next --limit 10
xuezh audio process-voice --file ./utterance.wav
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
