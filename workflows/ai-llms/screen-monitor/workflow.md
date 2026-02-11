# screen-monitor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/emasoudy/screen-monitor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/emasoudy/screen-monitor/SKILL.md)
> Category: AI & LLMs

---

## Description

Dual-mode screen sharing and analysis. Model-agnostic (Gemini/Claude/Qwen3-VL).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Dual-mode screen sharing and analysis. Model-agnostic (Gemini/Claude/Qwen3-VL).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run screen-monitor`)
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
You are executing the screen-monitor workflow. Use the following context:

Description: Dual-mode screen sharing and analysis. Model-agnostic (Gemini/Claude/Qwen3-VL).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: screen-monitor
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Screen Monitor

This skill provides two ways for the agent to see and interact with your screen.

## 🟢 Path A: Fast Share (WebRTC)
*Best for: Quick visual checks, restricted browsers, or non-technical environments.*

### Tools
- **`screen_share_link`**: Generates a local WebRTC portal URL.
- **`screen_analyze`**: Captures the current frame from the portal and analyzes it with vision.

**Usage:**
```bash
# Get the link
bash command:"{baseDir}/references/get-share-url.sh"

# Analyze
bash command:"{baseDir}/references/screen-analyze.sh"
```

---

## 🔵 Path B: Full Control (Browser Relay)
*Best for: Deep debugging, UI automation, and clicking/typing in tabs.*

### Setup
1. Run `clawdbot browser extension install`.
2. Load the unpacked extension from `clawdbot browser extension path`.
3. Click the Clawdbot icon in your Chrome toolbar to **Attach**.

### Tools
- **`browser action:snapshot`**: Take a precise screenshot of the attached tab.
- **`browser action:click`**: Interact with elements (requires `profile="chrome"`).

---

## Technical Details
- **Port**: 18795 (WebRTC Backend)
- **Files**: 
  - `web/screen-share.html`: The sharing portal.
  - `references/backend-endpoint.js`: Frame storage server.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
