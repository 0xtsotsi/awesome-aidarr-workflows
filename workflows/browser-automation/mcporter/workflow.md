# mcporter

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/mcporter/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/mcporter/SKILL.md)
> Category: Browser & Automation

---

## Description

Use the mcporter CLI to list, configure, auth, and call MCP servers/tools directly (HTTP or stdio), including ad-hoc servers, config edits, and CLI/type generation.

**Homepage:** http://mcporter.dev
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Use the mcporter CLI to list, configure, auth, and call MCP servers/tools directly (HTTP or stdio), including ad-hoc servers, config edits, and CLI/type generation.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run mcporter`)
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
You are executing the mcporter workflow. Use the following context:

Description: Use the mcporter CLI to list, configure, auth, and call MCP servers/tools directly (HTTP or stdio), including ad-hoc servers, config edits, and CLI/type generation.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: mcporter
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: http://mcporter.dev
```

---

## Original Skill Content



# mcporter

Use `mcporter` to work with MCP servers directly.

Quick start
- `mcporter list`
- `mcporter list <server> --schema`
- `mcporter call <server.tool> key=value`

Call tools
- Selector: `mcporter call linear.list_issues team=ENG limit:5`
- Function syntax: `mcporter call "linear.create_issue(title: \"Bug\")"`
- Full URL: `mcporter call https://api.example.com/mcp.fetch url:https://example.com`
- Stdio: `mcporter call --stdio "bun run ./server.ts" scrape url=https://example.com`
- JSON payload: `mcporter call <server.tool> --args '{"limit":5}'`

Auth + config
- OAuth: `mcporter auth <server | url> [--reset]`
- Config: `mcporter config list|get|add|remove|import|login|logout`

Daemon
- `mcporter daemon start|status|stop|restart`

Codegen
- CLI: `mcporter generate-cli --server <name>` or `--command <url>`
- Inspect: `mcporter inspect-cli <path> [--json]`
- TS: `mcporter emit-ts <server> --mode client|types`

Notes
- Config default: `./config/mcporter.json` (override with `--config`).
- Prefer `--output json` for machine-readable results.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
