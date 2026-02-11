# grok-imagine-render

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/raphbaph/grok-imagine-render/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/raphbaph/grok-imagine-render/SKILL.md)
> Category: AI & LLMs

---

## Description

Generate images using Grok (xAI) image generation API. Use when you need to create images from text prompts.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate images using Grok (xAI) image generation API. Use when you need to create images from text prompts.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run grok-imagine-render`)
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
You are executing the grok-imagine-render workflow. Use the following context:

Description: Generate images using Grok (xAI) image generation API. Use when you need to create images from text prompts.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: grok-imagine-render
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Grok Image Generation

## Setup

Add your API key to `~/.clawdbot/.env`:
```
GROK_API_KEY=xai-your-key-here
```

## Usage

Generate images with a simple prompt:

```
Generate a cute raccoon character with friendly smile
```

The skill will:
1. Read GROK_API_KEY from ~/.clawdbot/.env
2. Call Grok's image generation API
3. Save the image and return the path

## Options

- **Custom output path**: Add `--output /path/to/image.png`
- **Size**: `--size 512x512` (default: 1024x1024)

## Notes

- Uses grok-imagine-image model
- Images are saved to the workspace or specified path

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
