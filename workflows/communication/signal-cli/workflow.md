# signal-cli

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/pseudobun/signal-cli/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/pseudobun/signal-cli/SKILL.md)
> Category: Communication

---

## Description

Send Signal messages and look up Signal recipients via the local signal-cli installation on macOS. Use when the user asks to message someone on Signal, send a Signal text/attachment, list Signal contacts, or resolve a recipient by name/nickname/phone number.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Send Signal messages and look up Signal recipients via the local signal-cli installation on macOS. Use when the user asks to message someone on Signal, send a Signal text/attachment, list Signal contacts, or resolve a recipient by name/nickname/phone number.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run signal-cli`)
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
You are executing the signal-cli workflow. Use the following context:

Description: Send Signal messages and look up Signal recipients via the local signal-cli installation on macOS. Use when the user asks to message someone on Signal, send a Signal text/attachment, list Signal contacts, or resolve a recipient by name/nickname/phone number.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: signal-cli
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# signal-cli (Signal Messaging)

Use the local `signal-cli` binary.

## Preconditions

- `signal-cli` is installed and already linked/registered.
- For safety: confirm recipient + final message text with the user before sending.

## Quick patterns

### Discover available accounts

```bash
signal-cli listAccounts
```

### List contacts (JSON)

```bash
signal-cli -o json -u "+386..." listContacts
```

### Find a contact by name/nickname/number

Prefer the bundled script (handles fuzzy-ish matching + multiple matches):

```bash
python3 scripts/find_contact.py --account "+386..." --query "Name"
```

### Send a message

Prefer the bundled script (resolves contact names to numbers):

```bash
python3 scripts/send_message.py --account "+386..." --to "Name" --text "Heyo ..."
```

If `--to` is already a phone number in E.164 (e.g. `+386...`), it sends directly.

## Safety checklist (always)

- If resolving by name returns multiple matches, present options and ask the user which one.
- If message contains sensitive info, ask explicitly before sending via Signal.
- Default to `--service-environment live` (signal-cli default) and normal trust behavior.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
