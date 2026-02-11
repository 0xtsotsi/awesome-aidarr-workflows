# openclaw-echo-agent

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/krishna3554/openclaw-echo-agent/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/krishna3554/openclaw-echo-agent/SKILL.md)
> Category: Clawdbot Tools

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
**Trigger:** User-invocable (via `aidarr run openclaw-echo-agent`)
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
You are executing the openclaw-echo-agent workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openclaw-echo-agent
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# EchoAgent

EchoAgent is a minimal OpenClaw-compatible skill.

## What it does
- Accepts text input
- Uses a tool to process it
- Returns deterministic output

## Use case
This skill is intended as a reference example for building
and publishing OpenClaw agents.

## Entry point
agent.py

## Interoperability

This skill is designed to be used by other OpenClaw agents.

### Input
- text (string)

### Output
- result (string)

This agent can be safely chained inside multi-agent workflows.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
