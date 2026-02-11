# seedream-image-gen

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/owenrao/seedream-image-gen/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/owenrao/seedream-image-gen/SKILL.md)
> Category: AI & LLMs

---

## Description

Generate images via Seedream API (doubao-seedream models). Synchronous generation.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate images via Seedream API (doubao-seedream models). Synchronous generation.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run seedream-image-gen`)
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
You are executing the seedream-image-gen workflow. Use the following context:

Description: Generate images via Seedream API (doubao-seedream models). Synchronous generation.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: seedream-image-gen
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Seedream Image Generation

Generate images using Seedream API (synchronous, no polling needed).

## Generate Image

```bash
python3 {baseDir}/scripts/generate_image.py --prompt "your description" --filename "output.png"
```

Options:
- `--size`: `2K`, `4K`, or pixels (e.g., `2048x2048`)
- `--input-image`: Image URL for image-to-image/editing

## API Key

The `SEEDREAM_API_KEY` is automatically injected from `skills.entries.seedream-image-gen.apiKey` in `clawdbot.json`. You do NOT need to provide it manually.

## Notes

- Synchronous API: returns immediately when generation completes (no polling)
- Image URLs valid for 24 hours
- Script prints `MEDIA:` line for auto-attachment
- Include datetime in filenames to distinguish
- Models 4.5/4.0 support group image generation (multiple images per request)


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
