# stepfun-openrouter-v2

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mig6671/stepfun-openrouter-v2/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mig6671/stepfun-openrouter-v2/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Integrates StepFun AI models (Step-3.5 Flash, Step-3) via OpenRouter API. Free tier available. Features visible reasoning, fast responses, and multimodal capabilities.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Integrates StepFun AI models (Step-3.5 Flash, Step-3) via OpenRouter API. Free tier available. Features visible reasoning, fast responses, and multimodal capabilities.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run stepfun-openrouter-v2`)
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
You are executing the stepfun-openrouter-v2 workflow. Use the following context:

Description: Integrates StepFun AI models (Step-3.5 Flash, Step-3) via OpenRouter API. Free tier available. Features visible reasoning, fast responses, and multimodal capabilities.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: stepfun-openrouter-v2
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# StepFun via OpenRouter 🚀🧠

> **Fast, visible reasoning AI from StepFun — accessible via OpenRouter**

A complete OpenClaw skill that integrates StepFun's powerful reasoning models through OpenRouter's unified API.

## 🆓 FREE TIER AVAILABLE

Start using Step-3.5 Flash immediately, no credit card required!

## Quick Start

### 1. Get API Key
Visit https://openrouter.ai/keys and create a free API key.

### 2. Configure
```bash
export OPENROUTER_API_KEY="your-key-here"
```

### 3. Use
```bash
stepfun-cli "Hello!"
stepfun-cli --reasoning "Explain quantum computing"
```

## Available Models

| Model | Price | Description |
|-------|-------|-------------|
| stepfun/step-3.5-flash:free | **FREE** | Fast, efficient reasoning |
| stepfun/step-3.5-flash | ~$0.20/M tokens | Production-grade |
| stepfun-ai/step3 | Variable | Advanced multimodal |

## Features

- 🧠 Visible reasoning - see how AI thinks
- ⚡ Streaming responses
- 🖼️ Multimodal support
- 🔧 Full CLI with all options

## Installation

```bash
clawhub install stepfun-openrouter
```

## Links

- GitHub: https://github.com/mig6671/stepfun-openrouter
- ClawHub: https://clawhub.com/skills/stepfun-openrouter
- OpenRouter: https://openrouter.ai/models/stepfun/step-3.5-flash

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
