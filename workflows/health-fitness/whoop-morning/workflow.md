# whoop-morning

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/borahm/whoop-morning/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/borahm/whoop-morning/SKILL.md)
> Category: Health & Fitness

---

## Description

Check WHOOP recovery/sleep/strain each morning and send suggestions.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Check WHOOP recovery/sleep/strain each morning and send suggestions.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run whoop-morning`)
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
You are executing the whoop-morning workflow. Use the following context:

Description: Check WHOOP recovery/sleep/strain each morning and send suggestions.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: whoop-morning
category: Health & Fitness
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# whoop-morning

Morning WHOOP check-in:
- fetches your latest WHOOP data (Recovery, Sleep, Cycle/Strain)
- generates a short set of suggestions for the day

## Setup

### 1) Create WHOOP OAuth credentials

You already have:
- `WHOOP_CLIENT_ID`
- `WHOOP_CLIENT_SECRET`

Store these in `~/.clawdbot/.env`.

### 2) Authorize once (get refresh token)

Run:

```bash
/home/claw/clawd/skills/whoop-morning/bin/whoop-auth --scopes offline read:recovery read:sleep read:cycles read:profile
```

This prints an authorization URL.
Open it in your browser, approve, and paste the `code` back into the terminal.

The script will exchange it for tokens and write `WHOOP_REFRESH_TOKEN=...` to `~/.clawdbot/.env`.

### 3) Run the morning report

```bash
/home/claw/clawd/skills/whoop-morning/bin/whoop-morning
```

## Automation

Recommended: schedule with Gateway cron (daily, morning).
The cron job should run `whoop-morning` and send its output as a message.

## Notes

- This skill uses WHOOP OAuth2:
  - auth URL: `https://api.prod.whoop.com/oauth/oauth2/auth`
  - token URL: `https://api.prod.whoop.com/oauth/oauth2/token`
- WHOOP rotates refresh tokens; avoid running multiple refreshes in parallel.
- API availability/fields can change; if WHOOP returns 401/400 during token refresh, re-run `whoop-auth`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
