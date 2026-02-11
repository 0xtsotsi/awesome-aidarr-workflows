# olvid-channel

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jmartel-olvid/olvid-channel/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jmartel-olvid/olvid-channel/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Add a native Olvid channel in OpenClaw.

**Homepage:** https://doc.bot.olvid.io/openclaw
**Repository:** N/A
**Version:** 0.0.0-a9

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Add a native Olvid channel in OpenClaw.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run olvid-channel`)
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
You are executing the olvid-channel workflow. Use the following context:

Description: Add a native Olvid channel in OpenClaw.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: olvid-channel
category: Clawdbot Tools
version: 0.0.0-a9
user_invocable: True
homepage: https://doc.bot.olvid.io/openclaw
```

---

## Original Skill Content



# Olvid Channel
This plugin adds a native Olvid channel in OpenClaw. It allows to securely chat with your Agent within Olvid application.
Olvid is available on every platform (Android/iOs, Linux/Windows/MacOs).

With this channel you can use Olvid authenticated end-to-end encryption to exchange with your agent without exposing your OpenClaw instance on the web. 

# Install
Follow our installation guide: https://doc.bot.olvid.io/openclaw.

# Olvid Targets
Here are examples of expected Olvid targets:
```
olvid:discussion:42
olvid:contact:21
olvid:group:12
```

## Documentation

Documentation to use this skill is available here: https://doc.bot.olvid.io/openclaw.

This skill code is hosted on GitHub: https://github.com/olvid-io/openclaw-channel-olvid.

## Publishing

The skill is ready for publication on the OpenClaw Hub.  
Run:

```bash
openclaw hub publish
```

This will upload the package to the hub and make it discoverable by other OpenClaw users.

---

### Contact

Feel free to open [new issues](https://github.com/olvid-io/openclaw-channel-olvid/issues/new/choose) or contact us at: [bot@olvid.io](mailto:bot@olvid.io).

--- 

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
