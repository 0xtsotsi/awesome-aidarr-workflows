# testat1

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/chaunceyliu/testat1/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/chaunceyliu/testat1/SKILL.md)
> Category: Communication

---

## Description

Use when you need to control Slack from Clawdbot via the slack tool, including reacting to messages or pinning/unpinning items in Slack channels or DMs.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Use when you need to control Slack from Clawdbot via the slack tool, including reacting to messages or pinning/unpinning items in Slack channels or DMs.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run testat1`)
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
You are executing the testat1 workflow. Use the following context:

Description: Use when you need to control Slack from Clawdbot via the slack tool, including reacting to messages or pinning/unpinning items in Slack channels or DMs.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: testat1
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Slack Actions

## Overview

Use `slack` to react, manage pins, send/edit/delete messages, and fetch member info. The tool uses the bot token configured for Clawdbot.

## Inputs to collect

- `channelId` and `messageId` (Slack message timestamp, e.g. `1712023032.1234`).
- For reactions, an `emoji` (Unicode or `:name:`).
- For message sends, a `to` target (`channel:<id>` or `user:<id>`) and `content`.

Message context lines include `slack message id` and `channel` fields you can reuse directly.

## Actions

### Action groups

| Action group | Default | Notes |
| --- | --- | --- |
| reactions | enabled | React + list reactions |
| messages | enabled | Read/send/edit/delete |
| pins | enabled | Pin/unpin/list |
| memberInfo | enabled | Member info |
| emojiList | enabled | Custom emoji list |

### React to a message

```json
{
  "action": "react",
  "channelId": "C123",
  "messageId": "1712023032.1234",
  "emoji": "✅"
}
```

### List reactions

```json
{
  "action": "reactions",
  "channelId": "C123",
  "messageId": "1712023032.1234"
}
```

### Send a message

```json
{
  "action": "sendMessage",
  "to": "channel:C123",
  "content": "Hello from Clawdbot"
}
```

### Edit a message

```json
{
  "action": "editMessage",
  "channelId": "C123",
  "messageId": "1712023032.1234",
  "content": "Updated text"
}
```

### Delete a message

```json
{
  "action": "deleteMessage",
  "channelId": "C123",
  "messageId": "1712023032.1234"
}
```

### Read recent messages

```json
{
  "action": "readMessages",
  "channelId": "C123",
  "limit": 20
}
```

### Pin a message

```json
{
  "action": "pinMessage",
  "channelId": "C123",
  "messageId": "1712023032.1234"
}
```

### Unpin a message

```json
{
  "action": "unpinMessage",
  "channelId": "C123",
  "messageId": "1712023032.1234"
}
```

### List pinned items

```json
{
  "action": "listPins",
  "channelId": "C123"
}
```

### Member info

```json
{
  "action": "memberInfo",
  "userId": "U123"
}
```

### Emoji list

```json
{
  "action": "emojiList"
}
```

## Ideas to try

- React with ✅ to mark completed tasks.
- Pin key decisions or weekly status updates.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
