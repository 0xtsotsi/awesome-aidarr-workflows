# mcporter-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/livvux/mcporter-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/livvux/mcporter-skill/SKILL.md)
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
**Trigger:** User-invocable (via `aidarr run mcporter-skill`)
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
You are executing the mcporter-skill workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: mcporter-skill
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

---
name: mcporter
description: Use the mcporter CLI to list, configure, auth, and call MCP servers/tools directly (HTTP or stdio), including ad-hoc servers, config edits, and CLI/type generation.
homepage: https://github.com/pdxfinder/mcporter
metadata: {"clawdbot":{"emoji":"🔌","os":["darwin","linux","windows"],"requires":{"bins":["mcporter"]},"install":[{"id":"brew","kind":"brew","formula":"pdxfinder/tap/mcporter","bins":["mcporter"],"label":"Install mcporter (brew)"}]}}

# mcporter

Use `mcporter` to manage MCP (Model Context Protocol) servers and tools.

## Requirements
- `mcporter` CLI installed (via Homebrew: `brew install pdxfinder/tap/mcporter`)
- MCP server configuration in `~/.config/mcporter/`

## Common Commands

### List Configured Servers
```bash
mcporter list
```

### Authentication
```bash
mcporter auth --help
```

### Call MCP Tools
```bash
mcporter call <server-name> <tool-name> [arguments...]
```

### Generate CLI/Types
```bash
mcporter generate cli <server-name>
mcporter generate types <server-name>
```

### Config Management
```bash
mcporter config --help
```

## Notes
- mcporter supports both HTTP and stdio MCP servers
- Ad-hoc server creation is supported
- CLI generation creates typed wrappers for MCP tools
- Use `exec` tool to run mcporter commands

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
