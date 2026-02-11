# gemini

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/gemini/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/gemini/SKILL.md)
> Category: AI & LLMs

---

## Description

Gemini CLI for one-shot Q&A, summaries, and generation.

**Homepage:** https://ai.google.dev/
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Gemini CLI for one-shot Q&A, summaries, and generation.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run gemini`)
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
You are executing the gemini workflow. Use the following context:

Description: Gemini CLI for one-shot Q&A, summaries, and generation.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: gemini
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: https://ai.google.dev/
```

---

## Original Skill Content



# Gemini CLI

Use Gemini in one-shot mode with a positional prompt (avoid interactive mode).

Quick start
- `gemini "Answer this question..."`
- `gemini --model <name> "Prompt..."`
- `gemini --output-format json "Return JSON"`

Extensions
- List: `gemini --list-extensions`
- Manage: `gemini extensions <command>`

Notes
- If auth is required, run `gemini` once interactively and follow the login flow.
- Avoid `--yolo` for safety.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
