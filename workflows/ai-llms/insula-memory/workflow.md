# insula-memory

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/impkind/insula-memory/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/impkind/insula-memory/SKILL.md)
> Category: AI & LLMs

---

## Description

Internal state awareness for AI agents. Energy, mood, and interoception. Part of the AI Brain series.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Internal state awareness for AI agents. Energy, mood, and interoception. Part of the AI Brain series.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run insula-memory`)
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
You are executing the insula-memory workflow. Use the following context:

Description: Internal state awareness for AI agents. Energy, mood, and interoception. Part of the AI Brain series.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: insula-memory
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Insula Memory 🌡️

**Internal state awareness for AI agents.** Part of the AI Brain series.

## Status: 🚧 Under Development

This skill is being developed. Star/watch for updates!

## Concept

The insula processes interoception — awareness of internal bodily states. This skill will give AI agents:

- **State tracking** — energy, curiosity, engagement levels
- **Mood awareness** — not just performing emotions but having states
- **"Gut feelings"** — intuitive responses based on internal signals
- **Self-monitoring** — knowing when you're tired, overwhelmed, or energized

## AI Brain Series

| Part | Function | Status |
|------|----------|--------|
| [hippocampus](https://www.clawhub.ai/skills/hippocampus) | Memory formation, decay, reinforcement | ✅ Live |
| [amygdala-memory](https://www.clawhub.ai/skills/amygdala-memory) | Emotional processing | 🚧 Development |
| [basal-ganglia-memory](https://www.clawhub.ai/skills/basal-ganglia-memory) | Habit formation | 🚧 Development |
| [anterior-cingulate-memory](https://www.clawhub.ai/skills/anterior-cingulate-memory) | Conflict detection | 🚧 Development |
| **insula-memory** | Internal state awareness | 🚧 Development |

## Coming Soon

Based on neuroscience research on the insula's role in interoception and self-awareness.

---

*Built with ❤️ by the OpenClaw community*

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
