# llm-supervisor-agent

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dhardie/llm-supervisor-agent/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dhardie/llm-supervisor-agent/SKILL.md)
> Category: AI & LLMs

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run llm-supervisor-agent`)
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
You are executing the llm-supervisor-agent workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: llm-supervisor-agent
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# LLM Supervisor

Automatically switches OpenClaw between cloud and local Ollama models when rate limits occur.

## Features

- Detects rate-limit / overload errors from Anthropic/OpenAI
- Switches to a local Ollama fallback model
- Requires explicit confirmation before local code generation
- Supports manual commands:

### Commands

- `/llm status`
- `/llm switch cloud`
- `/llm switch local`

## Default Local Model

- `qwen2.5:7b`

## Safety

Local code generation requires the user to type:

`CONFIRM LOCAL CODE`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
