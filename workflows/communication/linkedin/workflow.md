# linkedin

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/biostartechnology/linkedin/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/biostartechnology/linkedin/SKILL.md)
> Category: Communication

---

## Description

LinkedIn automation via browser relay or cookies for messaging, profile viewing, and network actions.

**Homepage:** https://linkedin.com
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
LinkedIn automation via browser relay or cookies for messaging, profile viewing, and network actions.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run linkedin`)
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
You are executing the linkedin workflow. Use the following context:

Description: LinkedIn automation via browser relay or cookies for messaging, profile viewing, and network actions.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: linkedin
category: Communication
version: 1.0.0
user_invocable: True
homepage: https://linkedin.com
```

---

## Original Skill Content



# LinkedIn

Use browser automation to interact with LinkedIn - check messages, view profiles, search, and send connection requests.

## Connection Methods

### Option 1: Chrome Extension Relay (Recommended)
1. Open LinkedIn in Chrome and log in
2. Click the Clawdbot Browser Relay toolbar icon to attach the tab
3. Use `browser` tool with `profile="chrome"`

### Option 2: Isolated Browser
1. Use `browser` tool with `profile="clawd"` 
2. Navigate to linkedin.com
3. Log in manually (one-time setup)
4. Session persists for future use

## Common Operations

### Check Connection Status
```
browser action=snapshot profile=chrome targetUrl="https://www.linkedin.com/feed/"
```

### View Notifications/Messages
```
browser action=navigate profile=chrome targetUrl="https://www.linkedin.com/messaging/"
browser action=snapshot profile=chrome
```

### Search People
```
browser action=navigate profile=chrome targetUrl="https://www.linkedin.com/search/results/people/?keywords=QUERY"
browser action=snapshot profile=chrome
```

### View Profile
```
browser action=navigate profile=chrome targetUrl="https://www.linkedin.com/in/USERNAME/"
browser action=snapshot profile=chrome
```

### Send Message (confirm with user first!)
1. Navigate to messaging or profile
2. Use `browser action=act` with click/type actions
3. Always confirm message content before sending

## Safety Rules
- **Never send messages without explicit user approval**
- **Never accept/send connection requests without confirmation**
- **Avoid rapid automated actions** - LinkedIn is aggressive about detecting automation
- Rate limit: ~30 actions per hour max recommended

## Session Cookie Method (Advanced)
If browser relay isn't available, extract the `li_at` cookie from browser:
1. Open LinkedIn in browser, log in
2. DevTools → Application → Cookies → linkedin.com
3. Copy `li_at` value
4. Store securely for API requests

## Troubleshooting
- If logged out: Re-authenticate in browser
- If rate limited: Wait 24 hours, reduce action frequency
- If CAPTCHA: Complete manually in browser, then resume

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
