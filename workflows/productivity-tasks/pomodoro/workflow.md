# pomodoro

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/snail3d/pomodoro/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/snail3d/pomodoro/SKILL.md)
> Category: Productivity & Tasks

---

## Description

A beautiful Pomodoro timer with task tracking. Opens a clean, focused timer interface in your browser.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
A beautiful Pomodoro timer with task tracking. Opens a clean, focused timer interface in your browser.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run pomodoro`)
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
You are executing the pomodoro workflow. Use the following context:

Description: A beautiful Pomodoro timer with task tracking. Opens a clean, focused timer interface in your browser.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: pomodoro
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# 🍅 ClawDoro

A beautiful Pomodoro timer with task tracking. Built for focus.

![ClawDoro](https://snail3d.github.io/ClawDoro)

## Usage

```bash
# Start with default 27/5/15 min
clawdoro

# Custom focus time
clawdoro 50

# Full custom (focus/short/long)
clawdoro 50 10 30
```

Or just tell Clawd: **"Start ClawDoro"** or **"ClawDoro 45 minutes"**

## Features

- 🍅 Beautiful, distraction-free timer UI
- ⏱️ Customizable work/break durations (default 27 min - Clawd's pick!)
- 📝 Task list with localStorage persistence
- ⌨️ Keyboard shortcuts (Space = start/pause, R = reset)
- 🔊 3-pulse soothing chime on completion
- ☕ Fun "break time" surprise 😉
- 📱 Mobile responsive
- 💾 Everything persists between sessions

## How It Works

1. Opens a mini HTTP server on port 8765
2. Serves the beautiful ClawDoro UI
3. Auto-opens browser
4. Tasks & settings saved to localStorage

## Files

- `trigger.js` - Entry point that starts server and opens browser
- `timer.html` - The ClawDoro timer UI
- `SKILL.md` - This documentation

---

☕ **Support the work:** [Buy Me a Coffee](https://www.buymeacoffee.com/snail3d)

Built with 💜 by Clawd for Snail

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
