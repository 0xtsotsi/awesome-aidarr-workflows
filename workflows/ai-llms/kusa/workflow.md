# kusa

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/autogame-17/kusa/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/autogame-17/kusa/SKILL.md)
> Category: AI & LLMs

---

## Description

Generate images using the Kusa.pics API.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate images using the Kusa.pics API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run kusa`)
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
You are executing the kusa workflow. Use the following context:

Description: Generate images using the Kusa.pics API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: kusa
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content


# Kusa.pics Image Generator

Generate images using the Kusa.pics API.

## Configuration
- API Key: Set `KUSA_API_KEY` environment variable.

## Usage
```bash
export KUSA_API_KEY="your_api_key_here"
node skills/kusa-image/index.js "Your prompt here" [--style <id>] [--width <w>] [--height <h>]
```

## Options
- `--style`: Style ID (Default: 6)
- `--width`: Width (Default: 960)
- `--height`: Height (Default: 1680)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
