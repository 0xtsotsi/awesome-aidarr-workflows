# qwen-image

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/robin797860/qwen-image/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/robin797860/qwen-image/SKILL.md)
> Category: AI & LLMs

---

## Description

Generate images using Qwen Image API (Alibaba Cloud DashScope). Use when users request image generation with Chinese prompts or need high-quality AI-generated images from text descriptions.

**Homepage:** https://dashscope.aliyuncs.com/
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate images using Qwen Image API (Alibaba Cloud DashScope). Use when users request image generation with Chinese prompts or need high-quality AI-generated images from text descriptions.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run qwen-image`)
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
You are executing the qwen-image workflow. Use the following context:

Description: Generate images using Qwen Image API (Alibaba Cloud DashScope). Use when users request image generation with Chinese prompts or need high-quality AI-generated images from text descriptions.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: qwen-image
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: https://dashscope.aliyuncs.com/
```

---

## Original Skill Content



# Qwen Image

Generate high-quality images using Alibaba Cloud's Qwen Image API (通义万相).

## Usage

Generate an image (returns URL only):
```bash
uv run {baseDir}/scripts/generate_image.py --prompt "一副典雅庄重的对联悬挂于厅堂之中" --size "1664*928" --api-key sk-xxx
```

Generate and save locally:
```bash
uv run {baseDir}/scripts/generate_image.py --prompt "一副典雅庄重的对联悬挂于厅堂之中" --size "1664*928" --api-key sk-xxx
```

With custom model:
Support `qwen-image-max-2025-12-30` `qwen-image-plus-2026-01-09` `qwen-image-plus`
```bash
uv run {baseDir}/scripts/generate_image.py --prompt "a beautiful sunset over mountains" --model qwen-image-plus-2026-01-09 --api-key sk-xxx
```

## API Key
You can obtain the API key and run the image generation command in the following order.

- Get apiKey from `models.providers.bailian.apiKey` in `~/.openclaw/openclaw.json`
- Or get from `skills."qwen-image".apiKey` in `~/.openclaw/openclaw.json`
- Or get from `DASHSCOPE_API_KEY` environment variable
- Or Get your API key from: https://dashscope.console.aliyun.com/

## Options
**Sizes:**
- `1664*928` (default) - 16:9 landscape
- `1024*1024` - Square format
- `720*1280` - 9:16 portrait
- `1280*720` - 16:9 landscape (smaller)

**Additional flags:**
- `--negative-prompt "unwanted elements"` - Specify what to avoid
- `--no-prompt-extend` - Disable automatic prompt enhancement
- `--watermark` - Add watermark to generated image
- `--no-verify-ssl` - Disable SSL certificate verification (use when behind corporate proxy)

## Workflow

1. Execute the generate_image.py script with the user's prompt
2. Parse the script output and find the line starting with `MEDIA_URL:`
3. Extract the image URL from that line (format: `MEDIA_URL: https://...`)
4. Display the image to the user using markdown syntax: `![Generated Image](URL)`
5. Do NOT download or save the image unless the user specifically requests it

## Notes

- Supports both Chinese and English prompts
- By default, returns image URL directly without downloading
- The script prints `MEDIA_URL:` in the output - extract this URL and display it using markdown image syntax: `![generated image](URL)`
- Always look for the line starting with `MEDIA_URL:` in the script output and render the image for the user
- Default negative prompt helps avoid common AI artifacts
- Images are hosted on Alibaba Cloud OSS with temporary access URLs

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
