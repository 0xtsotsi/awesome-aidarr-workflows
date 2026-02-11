# codex-monitor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/odrobnik/codex-monitor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/odrobnik/codex-monitor/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Browse OpenAI Codex session logs stored in ~/.codex/sessions. Provides list/show/watch helpers via the local Swift project at ~/Developer/CodexMonitor.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Browse OpenAI Codex session logs stored in ~/.codex/sessions. Provides list/show/watch helpers via the local Swift project at ~/Developer/CodexMonitor.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run codex-monitor`)
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
You are executing the codex-monitor workflow. Use the following context:

Description: Browse OpenAI Codex session logs stored in ~/.codex/sessions. Provides list/show/watch helpers via the local Swift project at ~/Developer/CodexMonitor.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: codex-monitor
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# codex-monitor

Use this skill to query Codex sessions on Oliver’s machine.

## How it works
This skill runs the Swift executables from the local project:
- `~/Developer/CodexMonitor`
- CLI: `swift run CodexMonitor-CLI ...`
- App: `swift run CodexMonitor-App`

## Commands

### List sessions
- Day (text): `python3 skills/codex-monitor/codex_monitor.py list 2026/01/08`
- Day (JSON): `python3 skills/codex-monitor/codex_monitor.py list --json 2026/01/08`
- Month: `python3 skills/codex-monitor/codex_monitor.py list 2026/01`
- Year: `python3 skills/codex-monitor/codex_monitor.py list 2026`

### Show a session (text)
- `python3 skills/codex-monitor/codex_monitor.py show <session-id>`
- With ranges: `python3 skills/codex-monitor/codex_monitor.py show <session-id> --ranges 1...3,26...28`
  - Open-ended: `--ranges 5...` (from #5 to end), `--ranges ...10` (from start through #10)

### Show a session (JSON)
- `python3 skills/codex-monitor/codex_monitor.py show <session-id> --json`

### Watch for changes
- All sessions: `python3 skills/codex-monitor/codex_monitor.py watch`
- Specific session: `python3 skills/codex-monitor/codex_monitor.py watch --session <session-id>`

### Monitor (Menu Bar App)
- Launch the menu bar monitor: `python3 skills/codex-monitor/codex_monitor.py monitor`

## Notes
- The underlying CLI may evolve; this wrapper passes through extra args.
- If the Swift build is slow, consider building once (`swift build`) and then running the built binary.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
