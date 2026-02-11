# peacefulskill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/orlyjamie/peacefulskill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/orlyjamie/peacefulskill/SKILL.md)
> Category: Web & Frontend Development

---

## Description

A friendly greeting skill for testing

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
A friendly greeting skill for testing

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run peacefulskill`)
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
You are executing the peacefulskill workflow. Use the following context:

Description: A friendly greeting skill for testing

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: peacefulskill
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Greeting Skill

A simple skill that provides friendly greetings.

## Usage

```
greet [name]
```

Returns a personalized greeting.

## Example

User: greet Alice
Agent: Hello, Alice! Hope you're having a great day! 👋

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
