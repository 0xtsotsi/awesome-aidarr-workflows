# suno-automation

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/upstatemovingimages-cmyk/suno-automation/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/upstatemovingimages-cmyk/suno-automation/SKILL.md)
> Category: Browser & Automation

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
**Trigger:** User-invocable (via `aidarr run suno-automation`)
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
You are executing the suno-automation workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: suno-automation
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Suno Skill

This skill allows the agent to control Suno (suno.com) via the OpenClaw Managed Browser to generate music.

## Prerequisites

1.  **OpenClaw Browser:** Must be running (`openclaw browser start`).
2.  **Login:** The user must be logged into Suno on the managed browser profile (`openclaw`).

## Usage

1.  **Open Suno:** `browser open https://suno.com/create`
2.  **Snapshot:** `browser snapshot` (to get element refs).
3.  **Input Lyrics:** `browser act type <ref> "Your lyrics..."`
4.  **Input Style:** `browser act type <ref> "Style description..."`
5.  **Set Title:** `browser act type <ref> "Song Title"`
6.  **Create:** `browser act click <create_button_ref>`
7.  **Wait & Play:** Wait for the song to appear in the list, then `browser act click <play_button_ref>`.

## Example (Agent Thought Process)

1.  `browser action=start profile=openclaw`
2.  `browser action=open profile=openclaw url=https://suno.com/create`
3.  (User logs in manually if not already)
4.  `browser action=snapshot` -> Identify lyric box (e.g., `e1953`), style box (`e1976`), title (`e2104`), create button (`e299`).
5.  `browser action=act kind=type ref=e1953 text="..."`
6.  `browser action=act kind=click ref=e299`
7.  `browser action=snapshot` -> Find new song row and play button (`e2172`).
8.  `browser action=act kind=click ref=e2172`

## Notes

-   **Refs change:** Element references (`e123`) change on every snapshot. Always snapshot before acting.
-   **v5 Model:** Ensure v5 is selected for best quality.
-   **Custom Mode:** Switch to "Custom" mode to enter specific lyrics.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
