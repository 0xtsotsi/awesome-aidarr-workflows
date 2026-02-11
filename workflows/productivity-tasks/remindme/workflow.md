# remindme

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jacobthejacobs/remindme/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jacobthejacobs/remindme/SKILL.md)
> Category: Productivity & Tasks

---

## Description

⏰ simple Telegram reminders for OpenClaw.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** telegram, cron, reminders, productivity, schedule

---

## GOTCHA Framework

### G - Goals
⏰ simple Telegram reminders for OpenClaw.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run remindme`)
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
You are executing the remindme workflow. Use the following context:

Description: ⏰ simple Telegram reminders for OpenClaw.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: remindme
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# ⏰ Remind Me

Set reminders in Telegram using normal human language.

## 🚀 How to Use

Just type what you want and when:

- `/remindme drink water in 10m`
- `/remindme tomorrow 9am standup`
- `/remindme next monday call mom`
- `/remindme in 2 hours turn off oven`

No menus. No setup. No thinking.

## ✨ Why It’s Good

- **Natural language:** say it like a human
- **Fast:** reminder is scheduled instantly
- **Accurate:** runs on OpenClaw cron
- **Safe in groups:** reminders don’t get lost

## 🛠️ How It Works

Runs a background process that schedules reminders reliably through OpenClaw.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
