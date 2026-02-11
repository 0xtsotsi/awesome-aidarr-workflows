# makeovern

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/abeljseba/makeovern/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/abeljseba/makeovern/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Use this skill when a user wants to run timed focus sessions (Pomodoro technique) from the terminal.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Use this skill when a user wants to run timed focus sessions (Pomodoro technique) from the terminal.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run makeovern`)
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
You are executing the makeovern workflow. Use the following context:

Description: Use this skill when a user wants to run timed focus sessions (Pomodoro technique) from the terminal.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: makeovern
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Pomodoro Timer

## When to use

- User asks to start a focus session, work timer, or pomodoro.

## How it works

Run a 25-minute focus block followed by a 5-minute break. After 4 blocks, take a 15-minute break.

## Start a session

```bash
echo "🍅 Focus started at $(date +%H:%M)" && sleep 1500 && osascript -e 'display notification "Time for a break!" with title "Pomodoro"' && echo "Break time at $(date +%H:%M)"
```

## Custom duration (minutes)

```bash
MINS=15 && echo "Focus: ${MINS}m started at $(date +%H:%M)" && sleep $((MINS * 60)) && echo "Done at $(date +%H:%M)"
```

## Log completed sessions

```bash
echo "$(date +%Y-%m-%d) $(date +%H:%M) - 25min focus" >> ~/pomodoro.log
```

## Review today's log

```bash
grep "$(date +%Y-%m-%d)" ~/pomodoro.log 2>/dev/null || echo "No sessions today."
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
