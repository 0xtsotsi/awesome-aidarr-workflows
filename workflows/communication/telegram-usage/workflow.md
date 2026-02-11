# telegram-usage

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/c-drew/telegram-usage/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/c-drew/telegram-usage/SKILL.md)
> Category: Communication

---

## Description

Display session usage statistics (quota, session time, tokens, context)

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Display session usage statistics (quota, session time, tokens, context)

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run telegram-usage`)
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
You are executing the telegram-usage workflow. Use the following context:

Description: Display session usage statistics (quota, session time, tokens, context)

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: telegram-usage
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Telegram Usage Stats

Display comprehensive session usage statistics by running the handler script.

## What it does

Shows a quick status message with:
- **Quota Remaining**: Percentage of API quota left with visual indicator
- **Reset Timer**: Time remaining until quota resets

## How to use this skill

When the user asks for usage statistics, quota info, or session data:

```bash
node /home/drew-server/clawd/skills/telegram-usage/handler.js
```

This will output formatted HTML suitable for Telegram's parseMode.

## Output Format

The response is formatted as a clean Telegram message with:
- Section headers (bold)
- Clear percentages and time remaining
- Visual indicators (emoji)
- All in one message for quick reference

## Example Output

```
📊 API Usage

🔋 Quota: 🟢 47%
⏱️ Resets in: 53m
```

## Notes

- Pulls real-time data from `clawdbot models status`
- Updates on each invocation with current API quota values
- Uses plain text formatting for Telegram compatibility

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
