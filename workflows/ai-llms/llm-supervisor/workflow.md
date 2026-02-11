# llm-supervisor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dhardie/llm-supervisor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dhardie/llm-supervisor/SKILL.md)
> Category: AI & LLMs

---

## Description

Graceful rate limit handling with Ollama fallback. Notifies on rate limits, offers local model switch with confirmation for code tasks.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Graceful rate limit handling with Ollama fallback. Notifies on rate limits, offers local model switch with confirmation for code tasks.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run llm-supervisor`)
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
You are executing the llm-supervisor workflow. Use the following context:

Description: Graceful rate limit handling with Ollama fallback. Notifies on rate limits, offers local model switch with confirmation for code tasks.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: llm-supervisor
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# LLM Supervisor 🔮

Handles rate limits and model fallbacks gracefully.

## Behavior

### On Rate Limit / Overload Errors

When I encounter rate limits or overload errors from cloud providers (Anthropic, OpenAI):

1. **Tell the user immediately** — Don't silently fail or retry endlessly
2. **Offer local fallback** — Ask if they want to switch to Ollama
3. **Wait for confirmation** — Never auto-switch for code generation tasks

### Confirmation Required

Before using local models for code generation, ask:
> "Cloud is rate-limited. Switch to local Ollama (`qwen2.5:7b`)? Reply 'yes' to confirm."

For simple queries (chat, summaries), can switch without confirmation if user previously approved.

## Commands

### `/llm status`
Report current state:
- Which provider is active (cloud/local)
- Ollama availability and models
- Recent rate limit events

### `/llm switch local`
Manually switch to Ollama for the session.

### `/llm switch cloud`
Switch back to cloud provider.

## Using Ollama

```bash
# Check available models
ollama list

# Run a query
ollama run qwen2.5:7b "your prompt here"

# For longer prompts, use stdin
echo "your prompt" | ollama run qwen2.5:7b
```

## Installed Models

Check with `ollama list`. Configured default: `qwen2.5:7b`

## State Tracking

Track in memory during session:
- `currentProvider`: "cloud" | "local"  
- `lastRateLimitAt`: timestamp or null
- `localConfirmedForCode`: boolean

Reset to cloud at session start.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
