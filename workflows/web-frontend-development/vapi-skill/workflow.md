# vapi-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/colygon/vapi-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/colygon/vapi-skill/SKILL.md)
> Category: Web & Frontend Development

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run vapi-skill`)
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
You are executing the vapi-skill workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: vapi-skill
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Vapi (vapi.ai) — OpenClaw Skill

Use this skill when you need to manage **Vapi voice agents** (assistants), calls, phone numbers, tools, and webhooks from an OpenClaw agent.

This skill is **API-first** (Vapi REST) and optionally integrates with the **Vapi CLI** for MCP docs / local workflows.

## What you can do

- Create/update/list **assistants**
- Start/inspect/end **calls**
- Manage **phone numbers**
- Create/manage **tools** (function calling)
- Configure **webhooks** and inspect events

## Required secrets

Set one of:

- `VAPI_API_KEY` (recommended) — Vapi dashboard API key.

### How to provide the key (recommended)

- Store as a Gateway secret/env var (preferred), or
- Export in your shell before running helper scripts.

Never paste the key into public logs.

## Endpoints

Base URL:

- `https://api.vapi.ai`

Auth:

- `Authorization: Bearer $VAPI_API_KEY`

API reference:

- https://api.vapi.ai/api (Swagger)

## Tooling options

This skill supports **both** approaches; you can decide later per deployment.

- Set `VAPI_MODE=api` to prefer REST (default)
- Set `VAPI_MODE=cli` to prefer the Vapi CLI (interactive)

### Option A — REST via helper script (works everywhere)

This repo includes a tiny Node helper:

- `skills/vapi/bin/vapi-api.mjs`

Examples:

```bash
# list assistants
VAPI_API_KEY=... node skills/vapi/bin/vapi-api.mjs assistants:list

# create assistant
VAPI_API_KEY=... node skills/vapi/bin/vapi-api.mjs assistants:create \
  --name "Claw Con Concierge" \
  --modelProvider openai --model gpt-4o-mini \
  --voiceProvider 11labs --voiceId rachel

# start an outbound call (example shape; see swagger for required fields)
VAPI_API_KEY=... node skills/vapi/bin/vapi-api.mjs calls:create \
  --assistantId asst_xxx \
  --to "+14155551234" \
  --from "+14155559876"
```

### Option B — Vapi CLI (good for interactive ops)

If `VAPI_MODE=cli`, prefer using the CLI for management tasks and fall back to REST if the CLI isn’t installed.

Docs:
- https://docs.vapi.ai/cli
- https://github.com/VapiAI/cli

Install:

```bash
curl -sSL https://vapi.ai/install.sh | bash
vapi login
```

### Option C — MCP docs server for your IDE

This improves IDE assistance (Cursor/Windsurf/VSCode):
- https://docs.vapi.ai/cli/mcp

```bash
vapi mcp setup
```

## Agent usage guidance

When the user asks for Vapi changes:

1. Clarify **scope**: assistants vs phone numbers vs webhooks vs tool calls.
2. Prefer **read-only** queries first (list/get) before destructive changes.
3. When creating an assistant, ask for:
   - assistant name
   - model provider/model
   - voice provider/voice id
   - tools/function calling needs
   - webhook URL (if using server events)
4. When initiating calls, confirm:
   - to/from numbers
   - assistantId
   - compliance constraints (recording, consent)

## Files in this skill

- `skills/vapi/SKILL.md` — this file
- `skills/vapi/bin/vapi-api.mjs` — minimal REST helper

## Sources

- Vapi docs intro: https://docs.vapi.ai/quickstart/introduction
- Vapi CLI: https://github.com/VapiAI/cli
- Vapi MCP: https://docs.vapi.ai/cli/mcp
- Vapi API (Swagger): https://api.vapi.ai/api
- Example server (Node): https://github.com/VapiAI/example-server-javascript-node
- OpenClaw: https://github.com/openclaw/openclaw

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
