# inference-sh

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/okaris/inference-sh/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/okaris/inference-sh/SKILL.md)
> Category: AI & LLMs

---

## Description

Run 150+ AI apps via inference.sh CLI - image generation, video creation, LLMs, search, 3D, Twitter automation.
Models: FLUX, Veo, Gemini, Grok, Claude, Seedance, OmniHuman, Tavily, Exa, OpenRouter, and many more.
Use when running AI apps, generating images/videos, calling LLMs, web search, or automating Twitter.
Triggers: inference.sh, infsh, ai model, run ai, serverless ai, ai api, flux, veo, claude api,
image generation, video generation, openrouter, tavily, exa search, twitter api, grok


**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Run 150+ AI apps via inference.sh CLI - image generation, video creation, LLMs, search, 3D, Twitter automation.
Models: FLUX, Veo, Gemini, Grok, Claude, Seedance, OmniHuman, Tavily, Exa, OpenRouter, and many more.
Use when running AI apps, generating images/videos, calling LLMs, web search, or automating Twitter.
Triggers: inference.sh, infsh, ai model, run ai, serverless ai, ai api, flux, veo, claude api,
image generation, video generation, openrouter, tavily, exa search, twitter api, grok


### O - Orchestration
**Trigger:** User-invocable (via `aidarr run inference-sh`)
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
You are executing the inference-sh workflow. Use the following context:

Description: Run 150+ AI apps via inference.sh CLI - image generation, video creation, LLMs, search, 3D, Twitter automation.
Models: FLUX, Veo, Gemini, Grok, Claude, Seedance, OmniHuman, Tavily, Exa, OpenRouter, and many more.
Use when running AI apps, generating images/videos, calling LLMs, web search, or automating Twitter.
Triggers: inference.sh, infsh, ai model, run ai, serverless ai, ai api, flux, veo, claude api,
image generation, video generation, openrouter, tavily, exa search, twitter api, grok


Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: inference-sh
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# [inference.sh](https://inference.sh)

Run 150+ AI apps in the cloud with a simple CLI. No GPU required.

## Install CLI

```bash
curl -fsSL https://cli.inference.sh | sh
infsh login
```

## Quick Examples

```bash
# Generate an image
infsh app run falai/flux-dev-lora --input '{"prompt": "a cat astronaut"}'

# Generate a video
infsh app run google/veo-3-1-fast --input '{"prompt": "drone over mountains"}'

# Call Claude
infsh app run openrouter/claude-sonnet-45 --input '{"prompt": "Explain quantum computing"}'

# Web search
infsh app run tavily/search-assistant --input '{"query": "latest AI news"}'

# Post to Twitter
infsh app run x/post-tweet --input '{"text": "Hello from AI!"}'

# Generate 3D model
infsh app run infsh/rodin-3d-generator --input '{"prompt": "a wooden chair"}'
```

## Commands

| Task | Command |
|------|---------|
| List all apps | `infsh app list` |
| Search apps | `infsh app list --search "flux"` |
| Filter by category | `infsh app list --category image` |
| Get app details | `infsh app get google/veo-3-1-fast` |
| Generate sample input | `infsh app sample google/veo-3-1-fast --save input.json` |
| Run app | `infsh app run google/veo-3-1-fast --input input.json` |
| Run without waiting | `infsh app run <app> --input input.json --no-wait` |
| Check task status | `infsh task get <task-id>` |

## What's Available

| Category | Examples |
|----------|----------|
| **Image** | FLUX, Gemini 3 Pro, Grok Imagine, Seedream 4.5, Reve, Topaz Upscaler |
| **Video** | Veo 3.1, Seedance 1.5, Wan 2.5, OmniHuman, Fabric, HunyuanVideo Foley |
| **LLMs** | Claude Opus/Sonnet/Haiku, Gemini 3 Pro, Kimi K2, GLM-4, any OpenRouter model |
| **Search** | Tavily Search, Tavily Extract, Exa Search, Exa Answer, Exa Extract |
| **3D** | Rodin 3D Generator |
| **Twitter/X** | post-tweet, post-create, dm-send, user-follow, post-like, post-retweet |
| **Utilities** | Media merger, caption videos, image stitching, audio extraction |

## Related Skills

```bash
# Image generation (FLUX, Gemini, Grok, Seedream)
npx skills add inference-sh/skills@ai-image-generation

# Video generation (Veo, Seedance, Wan, OmniHuman)
npx skills add inference-sh/skills@ai-video-generation

# LLMs (Claude, Gemini, Kimi, GLM via OpenRouter)
npx skills add inference-sh/skills@llm-models

# Web search (Tavily, Exa)
npx skills add inference-sh/skills@web-search

# AI avatars & lipsync (OmniHuman, Fabric, PixVerse)
npx skills add inference-sh/skills@ai-avatar-video

# Twitter/X automation
npx skills add inference-sh/skills@twitter-automation

# Model-specific
npx skills add inference-sh/skills@flux-image
npx skills add inference-sh/skills@google-veo

# Utilities
npx skills add inference-sh/skills@image-upscaling
npx skills add inference-sh/skills@background-removal
```

## Reference Files

- [Authentication & Setup](references/authentication.md)
- [Discovering Apps](references/app-discovery.md)
- [Running Apps](references/running-apps.md)
- [CLI Reference](references/cli-reference.md)

## Documentation

- [Agent Skills Overview](https://inference.sh/blog/skills/agent-skills-overview) - The open standard for AI capabilities
- [Getting Started](https://inference.sh/docs/getting-started/introduction) - Introduction to inference.sh
- [What is inference.sh?](https://inference.sh/docs/getting-started/what-is-inference) - Platform overview
- [Apps Overview](https://inference.sh/docs/apps/overview) - Understanding the app ecosystem
- [CLI Setup](https://inference.sh/docs/extend/cli-setup) - Installing the CLI
- [Workflows vs Agents](https://inference.sh/blog/concepts/workflows-vs-agents) - When to use each
- [Why Agent Runtimes Matter](https://inference.sh/blog/agent-runtime/why-runtimes-matter) - Runtime benefits

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
