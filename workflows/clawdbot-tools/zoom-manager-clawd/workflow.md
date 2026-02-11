# zoom-manager-clawd

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/vnagin/zoom-manager-clawd/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/vnagin/zoom-manager-clawd/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Manage Zoom meetings via OAuth API. Create, list, delete, and update events.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Zoom meetings via OAuth API. Create, list, delete, and update events.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run zoom-manager-clawd`)
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
You are executing the zoom-manager-clawd workflow. Use the following context:

Description: Manage Zoom meetings via OAuth API. Create, list, delete, and update events.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: zoom-manager-clawd
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Zoom Manager

Manage your Zoom meetings directly from Clawdbot with this powerful, headless integration. This skill allows you to automate your meeting workflows without ever opening the Zoom dashboard.

### Key Features:
- **Full Meeting Lifecycle**: Create, list, update, and delete meetings using simple natural language or CLI commands.
- **Enterprise-Ready**: Built for Server-to-Server OAuth, ensuring secure and robust authentication.
- **Automated Recording**: Default support for cloud recording to make sure your sessions are always captured.
- **Developer Friendly**: Clean Node.js implementation that can be easily extended for custom automation flows (e.g., auto-scheduling after a CRM update).
- **Headless & Fast**: No browser required; interacts directly with the Zoom REST API v2.

## Setup

1. Create a **Server-to-Server OAuth** app in the [Zoom App Marketplace](https://marketplace.zoom.us/).
2. **Scopes Required**: In the Zoom App Marketplace (Scopes tab), add the following:
   - **Meetings**:
     - `meeting:read:admin` / `meeting:read:master` (View meetings)
     - `meeting:write:admin` / `meeting:write:master` (Create and update meetings)
     - `meeting:delete:admin` / `meeting:delete:master` (Delete meetings)
   - **Users**: `user:read:admin`
   - **Recordings**: `recording:read:admin`
3. Get your **Client ID**, **Client Secret**, and **Account ID** from the "App Credentials" tab.
4. Set them as environment variables in your Clawdbot config:
   - `ZOOM_CLIENT_ID`
   - `ZOOM_CLIENT_SECRET`
   - `ZOOM_ACCOUNT_ID`

## Commands

### List Meetings
```bash
node {baseDir}/scripts/zoom-cli.js list
```

### Create a Meeting
```bash
node {baseDir}/scripts/zoom-cli.js create "Meeting Topic" "2026-01-30T10:00:00Z" 60
```

### Update a Meeting
```bash
node {baseDir}/scripts/zoom-cli.js update <meeting_id> <new_start_time> <duration> "New Topic"
```

### Get Meeting Info
```bash
node {baseDir}/scripts/zoom-cli.js info <meeting_id>
```

### Delete a Meeting
```bash
node {baseDir}/scripts/zoom-cli.js delete <meeting_id>
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
