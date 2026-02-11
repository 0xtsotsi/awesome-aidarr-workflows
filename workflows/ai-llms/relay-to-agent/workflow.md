# relay-to-agent

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ericsantos/relay-to-agent/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ericsantos/relay-to-agent/SKILL.md)
> Category: AI & LLMs

---

## Description

Relay messages to AI agents on any OpenAI-compatible API. Supports multi-turn conversations with session management. List agents, send messages, reset sessions.

**Homepage:** https://platform.openai.com/docs/api-reference/chat
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Relay messages to AI agents on any OpenAI-compatible API. Supports multi-turn conversations with session management. List agents, send messages, reset sessions.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run relay-to-agent`)
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
You are executing the relay-to-agent workflow. Use the following context:

Description: Relay messages to AI agents on any OpenAI-compatible API. Supports multi-turn conversations with session management. List agents, send messages, reset sessions.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: relay-to-agent
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: https://platform.openai.com/docs/api-reference/chat
```

---

## Original Skill Content



# Relay To Agent

Send messages to AI agents on any OpenAI-compatible endpoint. Works with Connect Chat, OpenRouter, LiteLLM, vLLM, Ollama, and any service implementing the Chat Completions API.

## List available agents

```bash
node {baseDir}/scripts/relay.mjs --list
```

## Send a message to an agent

```bash
node {baseDir}/scripts/relay.mjs --agent linkedin-alchemist "Transform this article into a LinkedIn post"
```

## Multi-turn conversation

```bash
# First message
node {baseDir}/scripts/relay.mjs --agent connect-flow-ai "Analyze our latest campaign"

# Follow-up (same session, agent remembers context)
node {baseDir}/scripts/relay.mjs --agent connect-flow-ai "Compare with last month"
```

## Reset session

```bash
node {baseDir}/scripts/relay.mjs --agent linkedin-alchemist --reset "Start fresh with this article..."
```

## Options

| Flag | Description | Default |
|------|-------------|---------|
| `--agent ID` | Target agent identifier | (required) |
| `--reset` | Reset conversation before sending | off |
| `--list` | List available agents | — |
| `--session ID` | Custom session identifier | `default` |
| `--json` | Raw JSON output | off |

## Configuration

### agents.json

Configure agents and endpoint in `{baseDir}/agents.json`:

```json
{
  "baseUrl": "https://api.example.com/v1",
  "agents": [
    {
      "id": "my-agent",
      "name": "My Agent",
      "description": "What this agent does",
      "model": "model-id-on-the-api"
    }
  ]
}
```

### Environment variables

```bash
export RELAY_API_KEY="sk-..."          # API key (required)
export RELAY_BASE_URL="https://..."    # Override base URL from config
export RELAY_CONFIG="/path/to/agents.json"  # Custom config path
```

## Compatible Services

- **Connect Chat** — `api.connectchat.ai/api`
- **OpenRouter** — `openrouter.ai/api/v1`
- **LiteLLM** — `localhost:4000/v1`
- **vLLM** — `localhost:8000/v1`
- **Ollama** — `localhost:11434/v1`
- **Any OpenAI-compatible API**

## Session Management

Sessions are stored locally at `~/.cache/relay-to-agent/sessions/`. Each agent+session combination keeps up to 50 messages. Use `--session` for parallel conversations with the same agent.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
