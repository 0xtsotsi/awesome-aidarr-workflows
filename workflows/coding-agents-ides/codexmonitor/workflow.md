# codexmonitor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/odrobnik/codexmonitor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/odrobnik/codexmonitor/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

List/inspect/watch local OpenAI Codex sessions (CLI + VS Code) using the CodexMonitor Homebrew formula.

**Homepage:** https://github.com/Cocoanetics/CodexMonitor
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
List/inspect/watch local OpenAI Codex sessions (CLI + VS Code) using the CodexMonitor Homebrew formula.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run codexmonitor`)
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
You are executing the codexmonitor workflow. Use the following context:

Description: List/inspect/watch local OpenAI Codex sessions (CLI + VS Code) using the CodexMonitor Homebrew formula.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: codexmonitor
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: https://github.com/Cocoanetics/CodexMonitor
```

---

## Original Skill Content



# codexmonitor

Use `codexmonitor` to browse local OpenAI Codex sessions stored in `~/.codex/sessions`.

## Requirements
- macOS
- Codex installed and producing sessions (CLI and/or VS Code extension)

## Install (Homebrew)

```sh
brew tap cocoanetics/tap
brew install codexmonitor
```

## Common commands

- List sessions (day): `codexmonitor list 2026/01/08`
- List sessions (day, JSON): `codexmonitor list --json 2026/01/08`
- Show a session: `codexmonitor show <session-id>`
- Show with ranges: `codexmonitor show <session-id> --ranges 1...3,26...28`
- Show JSON: `codexmonitor show <session-id> --json`
- Watch all: `codexmonitor watch`
- Watch specific: `codexmonitor watch --session <session-id>`

## Notes
- `codexmonitor` reads sessions from `~/.codex/sessions/YYYY/MM/DD/`.
- Sessions can be resumed/appended by id via Codex: `codex exec resume <SESSION_ID> "message"`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
