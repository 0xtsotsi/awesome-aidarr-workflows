# parcel-package-tracking

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/gumadeiras/parcel-package-tracking/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/gumadeiras/parcel-package-tracking/SKILL.md)
> Category: CLI Utilities

---

## Description

Track and add deliveries via Parcel API.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Track and add deliveries via Parcel API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run parcel-package-tracking`)
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
You are executing the parcel-package-tracking workflow. Use the following context:

Description: Track and add deliveries via Parcel API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: parcel-package-tracking
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Parcel

Interact with the Parcel app API to track packages and add new deliveries.

## Configuration

This skill requires the `PARCEL_API_KEY` environment variable.
Get your key from [web.parcelapp.net](https://web.parcelapp.net).

## Tool: `parcel`

Control the Parcel API CLI.

### Parameters

- `action` (required): One of `list`, `add`, `carriers`.
- `mode`: For `list`, filter mode (`active` or `recent`). Default `recent`.
- `tracking`: For `add`, the tracking number.
- `carrier`: For `add`, the carrier code (e.g., `ups`, `usps`, `fedex`).
- `description`: For `add`, a description of the package.
- `notify`: For `add`, boolean to send push confirmation.
- `search`: For `carriers`, search string.

### Usage

**List Deliveries:**
```bash
# List recent deliveries
node ~/.clawdbot/skills/parcel/parcel-api.js list

# List active deliveries
node ~/.clawdbot/skills/parcel/parcel-api.js list --mode=active
```

**Add Delivery:**
```bash
node ~/.clawdbot/skills/parcel/parcel-api.js add \
  --tracking "1Z1234567890" \
  --carrier "ups" \
  --description "New Shoes" \
  --notify
```

**List Carriers:**
```bash
node ~/.clawdbot/skills/parcel/parcel-api.js carriers "ups"
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
