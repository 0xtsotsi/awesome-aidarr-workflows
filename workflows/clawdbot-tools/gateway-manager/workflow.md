# gateway-manager

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/autogame-17/gateway-manager/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/autogame-17/gateway-manager/SKILL.md)
> Category: Clawdbot Tools

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
**Trigger:** User-invocable (via `aidarr run gateway-manager`)
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
You are executing the gateway-manager workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: gateway-manager
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Gateway Manager

## Description
Handles administrative menu events from Feishu to manage the OpenClaw Gateway service.
Supports remote restart, status monitoring, and system diagnostics.

## Commands
- **Restart Gateway** (`restart_gateway`): Restarts the OpenClaw Gateway service (Master Only).
- **Status** (`status_gateway`): Returns the current status of the gateway (Active/Inactive).
- **System Info** (`system_info`): Displays server metrics (RAM, Uptime, Node version).
- **Test Button** (`test_menu_button`): Triggers a test response (Cute Mode).

## Security
- Critical operations (Restart) are restricted to the authorized Master ID defined in `USER.md`.
- Feedback is provided for unauthorized access attempts.

## Configuration
- Automatically discovers `USER.md` for authorization.
- Uses `feishu-card` for rich feedback.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
