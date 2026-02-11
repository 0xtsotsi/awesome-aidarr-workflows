# prompt-log

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/thesash/prompt-log/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/thesash/prompt-log/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Extract conversation transcripts from AI coding session logs (Clawdbot, Claude Code, Codex). Use when asked to export prompt history, session logs, or transcripts from .jsonl session files.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Extract conversation transcripts from AI coding session logs (Clawdbot, Claude Code, Codex). Use when asked to export prompt history, session logs, or transcripts from .jsonl session files.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run prompt-log`)
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
You are executing the prompt-log workflow. Use the following context:

Description: Extract conversation transcripts from AI coding session logs (Clawdbot, Claude Code, Codex). Use when asked to export prompt history, session logs, or transcripts from .jsonl session files.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: prompt-log
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Prompt Log

## Quick start

Run the bundled script on a session file:

```bash
scripts/extract.sh <session-file>
```

## Inputs

- **Session file**: A `.jsonl` session log from Clawdbot, Claude Code, or Codex.
- **Optional filters**: `--after` and `--before` ISO timestamps.
- **Optional output**: `--output` path for the markdown transcript.

## Outputs

- Writes a markdown transcript. Defaults to `.prompt-log/YYYY-MM-DD-HHMMSS.md` in the current project.

## Examples

```bash
scripts/extract.sh ~/.codex/sessions/2026/01/12/abcdef.jsonl
scripts/extract.sh ~/.claude/projects/my-proj/xyz.jsonl --after "2026-01-12T10:00:00" --before "2026-01-12T12:00:00"
scripts/extract.sh ~/.clawdbot/agents/main/sessions/123.jsonl --output my-transcript.md
```

## Dependencies

- Requires `jq` in PATH.
- Uses `gdate` if available on macOS; otherwise falls back to `date`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
