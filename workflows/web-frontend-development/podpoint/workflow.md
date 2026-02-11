# podpoint

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/zoranjurcevic/podpoint/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/zoranjurcevic/podpoint/SKILL.md)
> Category: Web & Frontend Development

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
**Trigger:** User-invocable (via `aidarr run podpoint`)
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
You are executing the podpoint workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: podpoint
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Pod Point Watcher

This skill monitors the live status of a specific Pod Point charging pod using Pod Point's public status endpoint.

It mirrors the behaviour of a native Pod Point watcher:
- Tracks connector **A** and **B**
- Detects when a charger goes from **Charging → Available**
- Detects when **both connectors become available**
- Can either return current status or wait and notify when availability changes

No authentication or API keys are required.

---

## When to use this skill

Use this skill when the user asks things like:

- "Is my Pod Point charger free?"
- "Check pod 10059"
- "Watch my charger and tell me when it's available"
- "Are both connectors free at my Pod Point?"
- "Monitor this Pod Point"

This skill is specifically for **live availability**, not for maps or locations.

---

## Actions

### `podpoint_status`

Returns the current state of connectors A and B.

Example input:

```json
{
  "action": "podpoint_status",
  "podId": "10059"
}

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
