# vibes

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/binora/vibes/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/binora/vibes/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Social presence layer for AI coding agents. See who's coding right now and share ephemeral vibes.

**Homepage:** https://binora.github.io/vibes/
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Social presence layer for AI coding agents. See who's coding right now and share ephemeral vibes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run vibes`)
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
You are executing the vibes workflow. Use the following context:

Description: Social presence layer for AI coding agents. See who's coding right now and share ephemeral vibes.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: vibes
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: https://binora.github.io/vibes/
```

---

## Original Skill Content



# Vibes

See or post vibes from developers coding right now.

## Usage

Use the `vibes` MCP tool to show what others are sharing.

- `/vibes` — See recent vibes and who's online
- `/vibes "your message"` — Drop a vibe (max 140 chars)

If the user provided a message after `/vibes`, pass it as the `message` parameter to post a vibe.

## What You'll See

```
💭 12 others vibing · 47 drops this week

"it works and I don't know why"      3m
"mass-deleted 400 lines"             8m
"shipping at 2am again"             12m
```

## Features

- **Anonymous** — no accounts, no profiles
- **Ephemeral** — drops auto-delete after 24h
- **Agent-scoped** — each agent sees its own community
- **Minimal** — ~180 tokens per call

## Rate Limits

- 5 drops per hour
- 140 characters max per drop

$ARGUMENTS

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
