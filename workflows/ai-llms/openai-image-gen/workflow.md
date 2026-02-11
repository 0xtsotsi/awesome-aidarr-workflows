# openai-image-gen

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/openai-image-gen/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/openai-image-gen/SKILL.md)
> Category: AI & LLMs

---

## Description

Batch-generate images via OpenAI Images API. Random prompt sampler + `index.html` gallery.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Batch-generate images via OpenAI Images API. Random prompt sampler + `index.html` gallery.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run openai-image-gen`)
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
You are executing the openai-image-gen workflow. Use the following context:

Description: Batch-generate images via OpenAI Images API. Random prompt sampler + `index.html` gallery.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openai-image-gen
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# OpenAI Image Gen

Generate a handful of “random but structured” prompts and render them via OpenAI Images API.

## Setup

- Needs env: `OPENAI_API_KEY`

## Run

From any directory (outputs to `~/Projects/tmp/...` when present; else `./tmp/...`):

```bash
python3 ~/Projects/agent-scripts/skills/openai-image-gen/scripts/gen.py
open ~/Projects/tmp/openai-image-gen-*/index.html
```

Useful flags:

```bash
python3 ~/Projects/agent-scripts/skills/openai-image-gen/scripts/gen.py --count 16 --model gpt-image-1.5
python3 ~/Projects/agent-scripts/skills/openai-image-gen/scripts/gen.py --prompt "ultra-detailed studio photo of a lobster astronaut" --count 4
python3 ~/Projects/agent-scripts/skills/openai-image-gen/scripts/gen.py --size 1536x1024 --quality high --out-dir ./out/images
```

## Output

- `*.png` images
- `prompts.json` (prompt ↔ file mapping)
- `index.html` (thumbnail gallery)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
