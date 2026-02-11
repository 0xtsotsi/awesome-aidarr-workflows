# shellphone-gateway

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/loserbcc/shellphone-gateway/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/loserbcc/shellphone-gateway/SKILL.md)
> Category: CLI Utilities

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
**Trigger:** User-invocable (via `aidarr run shellphone-gateway`)
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
You are executing the shellphone-gateway workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: shellphone-gateway
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# shellphone-gateway

Private WebSocket gateway for connecting iOS to your AI agents. No Telegram. No Discord. No middleman.

## What This Does

ShellPhone + OpenClaw Gateway creates a direct, encrypted line between your iPhone and your self-hosted AI bots.

- **Privacy-first**: Messages never touch third-party servers
- **Self-hosted**: Runs on your hardware
- **Auto-detects ollama**: Zero config if you have local LLMs
- **Free TTS/ASR**: Via ScrappyLabs (no account needed)

## Quick Start

### 1. Run the Gateway

```bash
# Docker (recommended)
git clone https://github.com/loserbcc/openclaw-gateway.git
cd openclaw-gateway
docker compose up

# Or Python
pip install openclaw-gateway
openclaw-gateway
```

### 2. Get the iOS App

Join the TestFlight beta: https://testflight.apple.com/join/BnjD4BEf

### 3. Connect

Scan the QR code from `http://localhost:8770/setup` or enter manually:
- **URL**: `wss://your-server:8770/gateway`
- **Token**: (printed on gateway startup)

## Links

- **TestFlight**: https://testflight.apple.com/join/BnjD4BEf
- **Gateway GitHub**: https://github.com/loserbcc/openclaw-gateway
- **ScrappyLabs**: https://scrappylabs.ai

## License

MIT — do whatever you want with it.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
