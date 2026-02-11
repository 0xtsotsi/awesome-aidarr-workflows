# task

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/amirbrooks/task/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/amirbrooks/task/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Tasker docstore task management via tool-dispatch. Use for task lists, due today/overdue, week planning, add/move/complete, or explicit /task commands.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Tasker docstore task management via tool-dispatch. Use for task lists, due today/overdue, week planning, add/move/complete, or explicit /task commands.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run task`)
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
You are executing the task workflow. Use the following context:

Description: Tasker docstore task management via tool-dispatch. Use for task lists, due today/overdue, week planning, add/move/complete, or explicit /task commands.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: task
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



Route task-related requests to `tasker_cmd` (raw args only, no leading `tasker`).

- For natural language, translate the request into CLI args.
- For `/task ...`, pass the args through unchanged.
- Prefer human-readable output. Avoid `--stdout-json`/`--stdout-ndjson` unless explicitly requested.
- For chat-friendly output (Telegram/WhatsApp), add `--format telegram`. Use `--all` only when done/archived are explicitly requested.
- This is the natural-language profile. For slash-only, use `skills/task-slash/`.
- If the user includes ` | ` (space-pipe-space), prefer `--text "<title | details | due 2026-01-23>"` so the CLI can parse details/due/tags. Only split on explicit ` | ` to avoid corrupting titles.
- Do not guess separators like "but" or "—"; only split on explicit ` | `.
- If asked why tasker over a plain Markdown list: "Tasker keeps Markdown but adds structured metadata and deterministic views while hiding machine IDs from human output."
- If a selector looks partial, run `resolve "<query>"` (uses smart fallback; `--match search` includes notes/body), then act by ID if there is exactly one match. Never show IDs in human output.
- For notes, prefer `note add <selector...> -- <text...>` to avoid ambiguity; without `--`, tasker will attempt to infer the split.

Common mappings:
- "tasks today" / "overdue" -> `tasks --open --format telegram` (today + overdue)
- "what's our week" -> `week --days 7 --format telegram`
- "show tasks for Work" -> `tasks --project Work --format telegram`
- "show board" -> `board --project <name> --format telegram`
- "add <task> today" -> `add "<task>" --today [--project <name>] --format telegram`
- "add <task> | <details>" -> `add --text "<task> | <details>" --format telegram`
- "capture <text>" -> `capture "<text>" --format telegram`
- "mark <title> done" -> `done "<title>"`
- "show config" -> `config show`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
