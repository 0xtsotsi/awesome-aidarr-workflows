# wyoming-clawdbot

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/vglafirov/wyoming-clawdbot/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/vglafirov/wyoming-clawdbot/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Wyoming Protocol bridge for Home Assistant voice assistant integration with Clawdbot.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Wyoming Protocol bridge for Home Assistant voice assistant integration with Clawdbot.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run wyoming-clawdbot`)
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
You are executing the wyoming-clawdbot workflow. Use the following context:

Description: Wyoming Protocol bridge for Home Assistant voice assistant integration with Clawdbot.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: wyoming-clawdbot
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Wyoming-Clawdbot

Bridge Home Assistant Assist voice commands to Clawdbot via Wyoming Protocol.

## What it does

- Receives voice commands from Home Assistant Assist
- Forwards them to Clawdbot for processing  
- Returns AI responses to be spoken by Home Assistant TTS

## Setup

1. Clone and run the server:
```bash
git clone https://github.com/vglafirov/wyoming-clawdbot.git
cd wyoming-clawdbot
docker compose up -d
```

2. Add Wyoming integration in Home Assistant:
   - Settings → Devices & Services → Add Integration
   - Search "Wyoming Protocol"
   - Enter host:port (e.g., `192.168.1.100:10600`)

3. Configure Voice Assistant pipeline to use "clawdbot" as Conversation Agent

## Requirements

- Clawdbot running on the same host
- Home Assistant with Wyoming integration
- Docker (recommended) or Python 3.11+

## Links

- GitHub: https://github.com/vglafirov/wyoming-clawdbot

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
