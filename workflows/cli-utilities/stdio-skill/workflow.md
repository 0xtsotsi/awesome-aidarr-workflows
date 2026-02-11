# stdio-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/safatinaztepe/stdio-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/safatinaztepe/stdio-skill/SKILL.md)
> Category: CLI Utilities

---

## Description

Stdin/stdout file inbox/outbox bridge for passing files to/from Clawdbot using an MCP stdio server. Use when you want a simple filesystem-backed dropbox: accept files into an inbox, move to tmp for processing, and emit deliverables to an outbox (or a specified path).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Stdin/stdout file inbox/outbox bridge for passing files to/from Clawdbot using an MCP stdio server. Use when you want a simple filesystem-backed dropbox: accept files into an inbox, move to tmp for processing, and emit deliverables to an outbox (or a specified path).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run stdio-skill`)
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
You are executing the stdio-skill workflow. Use the following context:

Description: Stdin/stdout file inbox/outbox bridge for passing files to/from Clawdbot using an MCP stdio server. Use when you want a simple filesystem-backed dropbox: accept files into an inbox, move to tmp for processing, and emit deliverables to an outbox (or a specified path).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: stdio-skill
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# stdio-skill

Implement and use a local MCP **stdio** server that provides a simple inbox/outbox workflow backed by directories on disk.

Paths (workspace-relative):
- `stdio/inbox/` — user drops inputs here
- `stdio/tmp/` — scratch area (move/copy inputs here for processing)
- `stdio/outbox/` — put deliverables here for pickup

## Start the MCP server (via mcporter)

This repo config should include an MCP server named `stdio-skill`.

- List tools:
  - `mcporter list stdio-skill --schema --timeout 120000 --json`

## Tooling model

Prefer:
1) `stdio-skill.stdio_list` to see what’s waiting.
2) `stdio-skill.stdio_read` (base64) to pull file contents.
3) `stdio-skill.stdio_move` to move an item to `tmp` once you’ve claimed it.
4) Write outputs with `stdio-skill.stdio_write` (base64) into `outbox` unless the user provided an explicit destination path.

No deprecated aliases: use the `stdio_*` tools only.

## Notes

- This skill is intentionally dumb/simple: it does not interpret file formats.
- It is safe-by-default: operations are restricted to the three directories above.
- For large files: prefer passing by path + moving files, not embedding giant base64 blobs in chat.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
