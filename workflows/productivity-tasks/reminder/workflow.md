# reminder

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ryanhong666/reminder/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ryanhong666/reminder/SKILL.md)
> Category: Productivity & Tasks

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
**Trigger:** User-invocable (via `aidarr run reminder`)
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
You are executing the reminder workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: reminder
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Reminder (secretary)

A lightweight personal secretary for OpenClaw:
- Tell it events in natural language (Chinese/English).
- It extracts structured info and stores it in your workspace (so Git/`claw-roam` can sync across devices).
- It schedules Telegram reminders using OpenClaw `cron`.


## What it does

- Capture events from chat (meetings / birthdays / deadlines)
- Store events in a **workspace data file** (easy to back up & sync via Git/`claw-roam`)
- Schedule Telegram reminders using OpenClaw `cron`
- Answer queries like “我最近有什么安排/计划？”

## Data (separated from skill)

This skill contains **no personal event data**.

User data lives in the workspace at:
- Events file: `~/.openclaw/workspace/reminders/events.yml`

Template (shipped with the skill):
- `skills/reminder/assets/events.template.yml`

## Config (env)

- `REMINDER_TZ` (default: `Asia/Shanghai`)
- `REMINDER_OFFSETS_MINUTES` (default: `1440,60,10` for 24h/1h/10m)

## Capture behavior

When user says something like:
- “后天上午10点有个会”
- “下个月2号我妈生日”
- “周五下午三点交报告”

Do:
1) Parse the event:
   - title
   - start datetime (Shanghai)
   - notes (optional)
   - reminders offsets (default 24h/1h/10m)
   - repeat (optional: yearly/monthly/weekly)
2) If key info is ambiguous (e.g. ‘后天’ date, ‘下个月’ which month, lunar birthday conversion, time missing), ask **only the minimal** clarifying question(s).
3) Write/update the event in `reminders/events.yml`.
4) Create `cron` jobs for each reminder time (delivery to current Telegram).

## Reply style

- After scheduling: reply briefly with the resolved datetime + confirmation.
- For cancellations/changes: confirm what was changed and whether cron jobs were removed/replaced.

## Queries

If user asks:
- “我最近有什么安排？”
- “下周有什么？”

Then read `reminders/events.yml`, compute upcoming items (Shanghai time), and summarize.

## Notes / safety

- Never commit machine-specific secrets (keep them in `LOCAL_CONFIG.md`, already gitignored).
- For lunar birthdays: store the canonical lunar date + the computed solar date for the target year; ask how to handle leap months when needed.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
