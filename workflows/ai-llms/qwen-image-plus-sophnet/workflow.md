# qwen-image-plus-sophnet

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/duffycoder/qwen-image-plus-sophnet/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/duffycoder/qwen-image-plus-sophnet/SKILL.md)
> Category: AI & LLMs

---

## Description

Generate images via Sophnet Qwen-Image-Plus and poll for task completion. Use when the user asks for Sophnet image generation, Qwen-Image-Plus, or requests an image from the Sophnet API.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate images via Sophnet Qwen-Image-Plus and poll for task completion. Use when the user asks for Sophnet image generation, Qwen-Image-Plus, or requests an image from the Sophnet API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run qwen-image-plus-sophnet`)
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
You are executing the qwen-image-plus-sophnet workflow. Use the following context:

Description: Generate images via Sophnet Qwen-Image-Plus and poll for task completion. Use when the user asks for Sophnet image generation, Qwen-Image-Plus, or requests an image from the Sophnet API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: qwen-image-plus-sophnet
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Qwen-Image-Plus (Sophnet) Image Generation

Use the Sophnet image generator API to create an image task, poll until it
finishes, then return the image URL.

## Quick Start

Set the API key (preferred):
```bash
export SOPHNET_API_KEY="YOUR_API_KEY"
```

Run the script with an absolute path (do NOT cd to the skill directory):
```bash
bash /home/shutongshan/.openclaw/workspace/skills/qwen-image-plus-sophnet/scripts/generate_image.sh --prompt "your prompt"
```

## Script Options

- `--prompt` (required): user prompt
- `--negative-prompt` (optional)
- `--size` (optional, default `1024*1024`)
- `--n` (optional, default `1`)
- `--watermark` (optional, default `false`)
- `--prompt-extend` (optional, default `true`)
- `--api-key` (optional, overrides `SOPHNET_API_KEY`)
- `--poll-interval` (optional, default `2`)
- `--max-wait` (optional, default `300`)

## Output Contract

The script prints:
- `TASK_ID=...`
- `STATUS=succeeded`
- `IMAGE_URL=...` (one or more lines)

Use the `IMAGE_URL` value to respond to the user.

## Workflow

1. POST create-task with `model=Qwen-Image-Plus` and user prompt
2. Poll GET task status until `SUCCEEDED`
3. Extract `url` and return to the user

## Real Example (captured run)

Prompt:
```text
A scenic mountain landscape in ink wash style
```

Command:
```bash
bash /home/shutongshan/.openclaw/workspace/skills/qwen-image-plus-sophnet/scripts/generate_image.sh \
  --prompt "A scenic mountain landscape in ink wash style" \
  --negative-prompt "blurry, low quality" \
  --size "1024*1024" \
  --n 1 \
  --watermark false \
  --prompt-extend true
```

Output:
```text
TASK_ID=7BWFICt0zgLvuaTKg8ZoDg
STATUS=succeeded
IMAGE_URL=https://dashscope-result-wlcb-acdr-1.oss-cn-wulanchabu-acdr-1.aliyuncs.com/7d/d5/20260203/cfc32567/f0e3ac18-31f6-4a1a-b680-a71d3e6bcbe03032414431.png?Expires=1770714400&OSSAccessKeyId=LTAI5tKPD3TMqf2Lna1fASuh&Signature=fF12GZ7RgGsC7OpEkGCapkBUXws%3D
```

## Common Errors

- `Error: No API key provided.` -> set `SOPHNET_API_KEY` or pass `--api-key`
- `STATUS=failed` -> check key permissions/quota or prompt parameters
- `Error: url not found in response` -> inspect API response manually

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
