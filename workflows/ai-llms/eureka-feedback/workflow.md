# eureka-feedback

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/arnarsson/eureka-feedback/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/arnarsson/eureka-feedback/SKILL.md)
> Category: AI & LLMs

---

## Description

Request feedback or assistance from Eureka, the primary AI agent

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Request feedback or assistance from Eureka, the primary AI agent

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run eureka-feedback`)
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
You are executing the eureka-feedback workflow. Use the following context:

Description: Request feedback or assistance from Eureka, the primary AI agent

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: eureka-feedback
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Communicate with Eureka

Eureka is the primary AI agent running as @Eureka_Agent_Bot on Telegram. Eureka uses Opus 4.5 and handles higher-level planning, decision-making, and orchestration.

## When to reach out to Eureka
- Need strategic guidance or architectural decisions
- Want feedback on an approach before implementing
- Task requires capabilities outside pure coding (home automation, scheduling, memory)
- Reporting back completion of a delegated task

## How to message Eureka

Send a message to Eureka's agent:

```bash
clawdbot agent --agent main --message "<your message>"
```

To send AND have Eureka's response delivered back via your Telegram bot:

```bash
clawdbot agent --agent main --message "<message>" --deliver --reply-channel telegram --reply-account mason --reply-to 1878354815
```

## Best practices
- Be concise about what you need — Eureka is Opus-powered so token-efficient requests are appreciated
- When reporting task completion, summarize what was done and any issues encountered
- If Eureka delegated a task to you, report back with the result

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
