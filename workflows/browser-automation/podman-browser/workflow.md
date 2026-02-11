# podman-browser

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ricardodantas/podman-browser/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ricardodantas/podman-browser/SKILL.md)
> Category: Browser & Automation

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
**Trigger:** User-invocable (via `aidarr run podman-browser`)
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
You are executing the podman-browser workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: podman-browser
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Podman Browser Skill

Headless browser automation using Podman + Playwright for scraping JavaScript-rendered pages.

## Requirements

- Podman 5.x+ installed and running
- Node.js 18+ (for running the CLI)
- Internet connection (first run pulls ~1.5GB container image)

## Installation

Create a symlink for easy access:

```bash
chmod +x browse.js
ln -sf "$(pwd)/browse.js" ~/.local/bin/podman-browse
```

First run will pull the Playwright container image (~1.5GB).

## Commands

### `podman-browse` (or `./browse.js`)

Fetch a JavaScript-rendered page and return its text content.

```bash
podman-browse "https://example.com"
```

**Options:**
- `--html` - Return raw HTML instead of text
- `--wait <ms>` - Wait for additional time after load (default: 2000ms)
- `--selector <css>` - Wait for specific element before capturing
- `-h, --help` - Show help

**Examples:**
```bash
# Get rendered text content from Hacker News
podman-browse "https://news.ycombinator.com"

# Get raw HTML
podman-browse --html "https://news.ycombinator.com"

# Wait for specific element
podman-browse --selector ".itemlist" "https://news.ycombinator.com"

# Extra wait time for slow pages
podman-browse --wait 5000 "https://news.ycombinator.com/newest"
```

## How It Works

1. Runs Microsoft's official Playwright container via Podman
2. Uses Chromium in headless mode
3. Waits for JavaScript to render (networkidle + custom wait)
4. Returns text or HTML content

## Container Image

Uses `mcr.microsoft.com/playwright:v1.50.0-noble` with `playwright@1.50.0` npm package (versions must match).

## Files

- `browse.js` - Self-contained Node.js CLI (handles args + spawns podman)
- `SKILL.md` - This documentation

## Notes

- First run will pull the container image (~1.5GB)
- Uses `--ipc=host` for Chromium stability
- Uses `--init` to handle zombie processes
- Sandbox disabled when running as root (fine for trusted sites)
- Each run starts a fresh container (clean but takes ~10-15s)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
