# grok-imagine

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/eddanger/grok-imagine/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/eddanger/grok-imagine/SKILL.md)
> Category: AI & LLMs

---

## Description

Generate images via xAI's Grok Imagine API. Use when the user wants to create AI-generated images using xAI/Grok, or when OpenAI image generation is unavailable.

**Homepage:** https://docs.x.ai/docs/api-reference#image-generation
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate images via xAI's Grok Imagine API. Use when the user wants to create AI-generated images using xAI/Grok, or when OpenAI image generation is unavailable.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run grok-imagine`)
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
You are executing the grok-imagine workflow. Use the following context:

Description: Generate images via xAI's Grok Imagine API. Use when the user wants to create AI-generated images using xAI/Grok, or when OpenAI image generation is unavailable.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: grok-imagine
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: https://docs.x.ai/docs/api-reference#image-generation
```

---

## Original Skill Content



# Grok Imagine

Generate images via xAI's Grok Imagine API.

## Run

```bash
node {baseDir}/scripts/gen.mjs --prompt "your image description"
```

## Examples

```bash
# Basic image generation
node {baseDir}/scripts/gen.mjs --prompt "a cyberpunk city at sunset"

# Multiple images
node {baseDir}/scripts/gen.mjs --prompt "a friendly robot" --count 4

# Custom output directory
node {baseDir}/scripts/gen.mjs --prompt "mountain landscape" --out-dir ./images

# Image editing (provide input image)
node {baseDir}/scripts/gen.mjs --prompt "add a rainbow to the sky" --input /path/to/image.png
```

## Models

- **grok-imagine-image**: Text-to-image and image editing (default)
- **grok-2-image**: Legacy image generation model

## Parameters

- `--prompt, -p`: Image description (required)
- `--count, -n`: Number of images to generate (default: 1)
- `--model, -m`: Model to use (default: grok-imagine-image)
- `--input, -i`: Input image path for editing tasks (optional)
- `--out-dir, -o`: Output directory (default: ./tmp/grok-imagine-<timestamp>)

## Output

- Generated images saved as PNG files
- `prompts.json` with prompt → file mapping
- `index.html` thumbnail gallery
- `MEDIA:` lines for OpenClaw auto-attach

## API Key

Set `XAI_API_KEY` environment variable, or configure in OpenClaw:
- `skills."grok-imagine".apiKey` in `~/.openclaw/openclaw.json`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
