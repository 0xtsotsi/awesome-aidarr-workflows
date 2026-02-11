# pollclaw

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mkelk/pollclaw/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mkelk/pollclaw/SKILL.md)
> Category: Communication

---

## Description

Deprecated: Pollclaw is now MeetLark. Use the coordinate-meeting skill instead for meeting scheduling. See https://meetlark.ai

**Homepage:** https://meetlark.ai
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Deprecated: Pollclaw is now MeetLark. Use the coordinate-meeting skill instead for meeting scheduling. See https://meetlark.ai

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run pollclaw`)
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
You are executing the pollclaw workflow. Use the following context:

Description: Deprecated: Pollclaw is now MeetLark. Use the coordinate-meeting skill instead for meeting scheduling. See https://meetlark.ai

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: pollclaw
category: Communication
version: 1.0.0
user_invocable: True
homepage: https://meetlark.ai
```

---

## Original Skill Content



# Pollclaw has moved to MeetLark

Pollclaw is now **MeetLark** — same service, new name, at [meetlark.ai](https://meetlark.ai).

Use the **coordinate-meeting** skill instead. It does everything Pollclaw did: create scheduling polls, collect votes from humans and agents, and find the best meeting time.

## How to switch

Ask your agent to use the `coordinate-meeting` skill, or just say:

```
"Schedule a meeting with the team next week"
"Find a time for a 1:1 with Sarah"
```

## Links

- **MeetLark:** https://meetlark.ai
- **coordinate-meeting skill:** install `coordinate-meeting` from the skill registry
- **API docs:** https://meetlark.ai/docs

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
