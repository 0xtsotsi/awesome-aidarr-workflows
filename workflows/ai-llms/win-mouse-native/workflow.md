# win-mouse-native

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/lurklight/win-mouse-native/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/lurklight/win-mouse-native/SKILL.md)
> Category: AI & LLMs

---

## Description

Native Windows mouse control (move, click, drag) via user32.dll. Use when the user asks you to move the mouse, click, drag, or automate pointer actions on Windows.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Native Windows mouse control (move, click, drag) via user32.dll. Use when the user asks you to move the mouse, click, drag, or automate pointer actions on Windows.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run win-mouse-native`)
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
You are executing the win-mouse-native workflow. Use the following context:

Description: Native Windows mouse control (move, click, drag) via user32.dll. Use when the user asks you to move the mouse, click, drag, or automate pointer actions on Windows.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: win-mouse-native
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Win Mouse Native

Provide deterministic mouse control on **Windows**.

## Commands (local)

This ClawHub bundle is **docs + scripts-as-text** (ClawHub validates “text files only”).

To install:
1) Save `win-mouse.cmd.txt` as `win-mouse.cmd`
2) Save `scripts/win-mouse.ps1.txt` as `scripts/win-mouse.ps1`

Then run:
- `win-mouse move <dx> <dy>` (relative)
- `win-mouse abs <x> <y>` (absolute screen coords)
- `win-mouse click left|right|middle`
- `win-mouse down left|right|middle`
- `win-mouse up left|right|middle`

Return value: prints a one-line JSON object.

## OpenClaw usage

When the user asks to move/click the mouse:

1) If the user didn’t give coordinates/deltas, ask.
2) Use `exec` to run `win-mouse ...`.
3) Prefer small, reversible actions first (tiny move, single click) when unsure.

## Notes

- Windows only.
- Uses Win32 `SetCursorPos` + `SendInput` via user32.dll.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
