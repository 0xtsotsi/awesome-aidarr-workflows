# playwright-cli

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/gumadeiras/playwright-cli/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/gumadeiras/playwright-cli/SKILL.md)
> Category: Browser & Automation

---

## Description

Browser automation via Playwright CLI. Open pages, interact with elements, take screenshots, and more. Ideal for coding agents and automated testing workflows.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Browser automation via Playwright CLI. Open pages, interact with elements, take screenshots, and more. Ideal for coding agents and automated testing workflows.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run playwright-cli`)
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
You are executing the playwright-cli workflow. Use the following context:

Description: Browser automation via Playwright CLI. Open pages, interact with elements, take screenshots, and more. Ideal for coding agents and automated testing workflows.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: playwright-cli
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Playwright CLI

Browser automation via Playwright. Token-efficient CLI for coding agents.

## Installation

```bash
npm install -g @playwright/mcp@latest
playwright-cli --help
```

## Core Commands

| Command | Description |
|---------|-------------|
| `playwright-cli open <url>` | Open URL in browser |
| `playwright-cli close` | Close the page |
| `playwright-cli type <text>` | Type text into editable element |
| `playwright-cli click <ref> [button]` | Click on element |
| `playwright-cli dblclick <ref> [button]` | Double click |
| `playwright-cli fill <ref> <text>` | Fill text into field |
| `playwright-cli drag <startRef> <endRef>` | Drag and drop |
| `playwright-cli hover <ref>` | Hover over element |
| `playwright-cli check <ref>` | Check checkbox/radio |
| `playwright-cli uncheck <ref>` | Uncheck checkbox |
| `playwright-cli select <ref> <val>` | Select dropdown option |
| `playwright-cli snapshot` | Capture page snapshot for refs |

## Navigation

```bash
playwright-cli go-back           # Go back
playwright-cli go-forward        # Go forward
playwright-cli reload            # Reload page
```

## Keyboard & Mouse

```bash
playwright-cli press <key>       # Press key (a, arrowleft, enter...)
playwright-cli keydown <key>     # Key down
playwright-cli keyup <key>       # Key up
playwright-cli mousemove <x> <y> # Move mouse
playwright-cli mousedown [button] # Mouse down
playwright-cli mouseup [button]   # Mouse up
playwright-cli mousewheel <dx> <dy> # Scroll
```

## Save & Export

```bash
playwright-cli screenshot [ref]  # Screenshot page or element
playwright-cli pdf               # Save as PDF
```

## Tabs

```bash
playwright-cli tab-list          # List all tabs
playwright-cli tab-new [url]     # Open new tab
playwright-cli tab-close [index] # Close tab
playwright-cli tab-select <index> # Switch tab
```

## DevTools

```bash
playwright-cli console [min-level]  # View console messages
playwright-cli network              # View network requests
playwright-cli run-code <code>      # Run JS snippet
playwright-cli tracing-start        # Start trace
playwright-cli tracing-stop         # Stop trace
```

## Sessions

```bash
playwright-cli session-list         # List sessions
playwright-cli session-stop [name]  # Stop session
playwright-cli session-stop-all     # Stop all
playwright-cli session-delete [name] # Delete session data
```

## Headed Mode

```bash
playwright-cli open https://example.com --headed
```

## Examples

```bash
# Open and interact
playwright-cli open https://example.com
playwright-cli type "search query"
playwright-cli press Enter
playwright-cli screenshot

# Use sessions
playwright-cli open https://site1.com
playwright-cli --session=project-a open https://site2.com
```

## Environment Variables

| Variable | Description |
|----------|-------------|
| `PLAYWRIGHT_MCP_BROWSER` | Browser: chrome, firefox, webkit, msedge |
| `PLAYWRIGHT_MCP_HEADLESS` | Run headless (default: headed) |
| `PLAYWRIGHT_MCP_ALLOWED_HOSTS` | Comma-separated allowed hosts |
| `PLAYWRIGHT_MCP_CONFIG` | Path to config file |

## Configuration

Create `playwright-cli.json` for persistent settings:

```json
{
  "browser": {
    "browserName": "chromium",
    "headless": false
  },
  "outputDir": "./playwright-output",
  "console": {
    "level": "info"
  }
}
```

## Notes

- **Cross-platform** — requires Node.js 18+ (Linux, macOS, Windows)
- Sessions persist cookies/storage by default
- Use `--session` flag for isolated browser instances
- Snapshots return element refs for subsequent commands

## Source

https://github.com/microsoft/playwright-cli

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
