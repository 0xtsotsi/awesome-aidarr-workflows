# pushover-notify

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/digitallyborn/pushover-notify/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/digitallyborn/pushover-notify/SKILL.md)
> Category: Communication

---

## Description

Send push notifications to your phone via Pushover (pushover.net). Use when you want reliable out-of-band alerts from OpenClaw: reminders, monitoring alerts, cron/heartbeat summaries, or 'notify me when X happens' workflows.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Send push notifications to your phone via Pushover (pushover.net). Use when you want reliable out-of-band alerts from OpenClaw: reminders, monitoring alerts, cron/heartbeat summaries, or 'notify me when X happens' workflows.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run pushover-notify`)
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
You are executing the pushover-notify workflow. Use the following context:

Description: Send push notifications to your phone via Pushover (pushover.net). Use when you want reliable out-of-band alerts from OpenClaw: reminders, monitoring alerts, cron/heartbeat summaries, or 'notify me when X happens' workflows.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: pushover-notify
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Pushover Notify

Send push notifications through the Pushover API using a small Node script.

## Setup (one-time)

1) Create a Pushover application token and get your user key:
- App token: https://pushover.net/apps/build
- User key: shown on your Pushover dashboard

2) Provide credentials to the runtime (do **not** hardcode into this skill):
- `PUSHOVER_APP_TOKEN`
- `PUSHOVER_USER_KEY`

3) (Optional) set defaults:
- `PUSHOVER_DEVICE` (device name)
- `PUSHOVER_SOUND`

## Send a notification

Use the bundled script:

```bash
PUSHOVER_APP_TOKEN=... PUSHOVER_USER_KEY=... \
  node skills/pushover-notify/scripts/pushover_send.js \
  --title "OpenClaw" \
  --message "Hello from Ted" \
  --priority 0
```

Optional fields:
- `--url "https://..."` and `--url-title "Open"`
- `--sound "pushover"`
- `--device "iphone"`
- `--priority -1|0|1|2`

Emergency priority example:

```bash
PUSHOVER_APP_TOKEN=... PUSHOVER_USER_KEY=... \
  node skills/pushover-notify/scripts/pushover_send.js \
  --title "ALERT" \
  --message "Something is on fire" \
  --priority 2 --retry 60 --expire 3600
```

## Notes

- If you need API field details, read: `references/pushover-api.md`.
- For recurring alerts, prefer `cron` to schedule reminders; the cron job text can instruct Ted to run this skill.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
