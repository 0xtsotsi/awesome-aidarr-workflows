# yboard-operator

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/zonder/yboard-operator/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/zonder/yboard-operator/SKILL.md)
> Category: PDF & Documents

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
**Trigger:** User-invocable (via `aidarr run yboard-operator`)
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
You are executing the yboard-operator workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: yboard-operator
category: PDF & Documents
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# YBoard Operator

Operate **yboard.online** to edit video/presentation plans.

## What this skill enables
- Navigate scenes (including scrolling the Scenes sidebar)
- Switch View/Edit/Markdown modes
- Edit fields: title, goal, visual guide, narration, assets required
- Add/replace scene illustrations using **Draw Custom Image**
- Enforce clean visuals (avoid text overlap; prefer text-free images)

## Workflow (reliable)
1) Ensure Browser Relay is attached to the yboard tab.
2) Switch to **Edit** mode.
3) Select the target scene from the **Scenes** sidebar.
4) Edit text fields.
5) Add/replace an image: **Draw Custom Image → Apply**.
6) QA: correct scene number/title + image attached + visuals readable.

## Illustration rules (no overlap)
- Prefer **no text inside images**.
- One clear “hero visual” per scene.
- Use simple icons/shapes: crate, cursor click, sound waves, HP bar, chunks.

## Common patterns
- Click/impact: cursor + crate + sound waves
- Skins: 3 stages (clean→damaged→broken)
- Dents: crack line + dent circle
- HP: bar above crate (green→yellow→red)
- Break: chunks + outward arrows

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
