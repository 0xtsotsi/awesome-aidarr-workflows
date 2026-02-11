# relayplane

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/relayplane/relayplane/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/relayplane/relayplane/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Cut API costs 40-60% with intelligent model routing. Auto-routes simple tasks to cheaper models.

**Homepage:** https://relayplane.com
**Repository:** N/A
**Version:** 3.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Cut API costs 40-60% with intelligent model routing. Auto-routes simple tasks to cheaper models.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run relayplane`)
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
You are executing the relayplane workflow. Use the following context:

Description: Cut API costs 40-60% with intelligent model routing. Auto-routes simple tasks to cheaper models.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: relayplane
category: Web & Frontend Development
version: 3.0.0
user_invocable: True
homepage: https://relayplane.com
```

---

## Original Skill Content



# RelayPlane

**Cut your AI API costs by 40-60%** with intelligent model routing.

## What It Does

RelayPlane is a local proxy that routes your LLM requests to the optimal model based on task complexity. Simple tasks go to cheaper models (Haiku), complex reasoning stays on premium models (Opus).

## Installation

Install the proxy globally:

```bash
npm install -g @relayplane/proxy
```

## Quick Start

```bash
# 1. Start the proxy
relayplane-proxy

# 2. Point OpenClaw at it (add to your shell config)
export ANTHROPIC_BASE_URL=http://localhost:3001
export OPENAI_BASE_URL=http://localhost:3001

# 3. Run OpenClaw normally - requests now route through RelayPlane
```

## Commands

Once installed, use the CLI directly:

| Command | Description |
|---------|-------------|
| `relayplane-proxy` | Start the proxy server |
| `relayplane-proxy stats` | View usage and cost breakdown |
| `relayplane-proxy telemetry off` | Disable telemetry |
| `relayplane-proxy telemetry status` | Check telemetry setting |
| `relayplane-proxy --help` | Show all options |

## Configuration

The proxy runs on `localhost:3001` by default. Configure via CLI flags:

```bash
relayplane-proxy --port 8080        # Custom port
relayplane-proxy --host 0.0.0.0     # Bind to all interfaces
relayplane-proxy --offline          # No telemetry, no network except LLM APIs
relayplane-proxy --audit            # Show telemetry payloads before sending
```

## Environment Variables

Set your API keys before starting:

```bash
export ANTHROPIC_API_KEY=sk-ant-...
export OPENAI_API_KEY=sk-...
# Optional: Google, xAI
export GEMINI_API_KEY=...
export XAI_API_KEY=...
```

## Privacy

- **Your prompts stay local** — never sent to RelayPlane
- **Anonymous telemetry** — only token counts, latency, model used
- **Opt-out anytime** — `relayplane-proxy telemetry off`
- **Fully offline mode** — `relayplane-proxy --offline`

## Links

- **Docs:** https://relayplane.com/docs
- **GitHub:** https://github.com/RelayPlane/proxy
- **npm:** https://www.npmjs.com/package/@relayplane/proxy

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
