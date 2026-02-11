# imsg

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/imsg/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/imsg/SKILL.md)
> Category: Communication

---

## Description

iMessage/SMS CLI for listing chats, history, watch, and sending.

**Homepage:** https://imsg.to
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
iMessage/SMS CLI for listing chats, history, watch, and sending.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run imsg`)
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
You are executing the imsg workflow. Use the following context:

Description: iMessage/SMS CLI for listing chats, history, watch, and sending.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: imsg
category: Communication
version: 1.0.0
user_invocable: True
homepage: https://imsg.to
```

---

## Original Skill Content



# imsg

Use `imsg` to read and send Messages.app iMessage/SMS on macOS.

Requirements
- Messages.app signed in
- Full Disk Access for your terminal
- Automation permission to control Messages.app (for sending)

Common commands
- List chats: `imsg chats --limit 10 --json`
- History: `imsg history --chat-id 1 --limit 20 --attachments --json`
- Watch: `imsg watch --chat-id 1 --attachments`
- Send: `imsg send --to "+14155551212" --text "hi" --file /path/pic.jpg`

Notes
- `--service imessage|sms|auto` controls delivery.
- Confirm recipient + message before sending.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
