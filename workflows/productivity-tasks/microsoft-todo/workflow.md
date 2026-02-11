# microsoft-todo

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/underwear/microsoft-todo/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/underwear/microsoft-todo/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Manage Microsoft To Do tasks via the `todo` CLI. Use when user wants to add, list, complete, remove tasks, manage subtasks (steps), notes, or organize task lists.

**Homepage:** https://github.com/underwear/microsoft-todo-cli
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Microsoft To Do tasks via the `todo` CLI. Use when user wants to add, list, complete, remove tasks, manage subtasks (steps), notes, or organize task lists.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run microsoft-todo`)
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
You are executing the microsoft-todo workflow. Use the following context:

Description: Manage Microsoft To Do tasks via the `todo` CLI. Use when user wants to add, list, complete, remove tasks, manage subtasks (steps), notes, or organize task lists.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: microsoft-todo
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: https://github.com/underwear/microsoft-todo-cli
```

---

## Original Skill Content



# Microsoft To Do CLI

Manage tasks in Microsoft To Do using the `todo` command.

## References

- `references/setup.md` (Azure app registration + OAuth configuration)

## Prerequisites

1. `todo` CLI installed (`pip install microsoft-todo-cli`)
2. Microsoft Azure app registered (see `references/setup.md`)
3. Credentials configured at `~/.config/microsoft-todo-cli/keys.yml`
4. First run completes OAuth flow in browser

## Commands

### Tasks

```bash
# List tasks
todo tasks --json                        # Default list
todo tasks Work --json                   # Specific list
todo tasks --due-today --json            # Due today
todo tasks --overdue --json              # Past due
todo tasks --important --json            # High priority
todo tasks --completed --json            # Done tasks
todo tasks --all --json                  # Everything

# Create task
todo new "Task name" --json              # Basic
todo new "Task" -l Work --json           # In specific list
todo new "Task" -d tomorrow --json       # With due date
todo new "Task" -r 2h --json             # With reminder
todo new "Task" -d mon -r 9am --json     # Due Monday, remind 9am
todo new "Task" -I --json                # Important
todo new "Task" -R daily --json          # Recurring daily
todo new "Task" -R weekly:mon,fri --json # Specific days
todo new "Task" -S "Step 1" -S "Step 2" --json  # With subtasks
todo new "Task" -N "Note content" --json      # With note

# Update task
todo update "Task" --title "New" --json
todo update "Task" -d friday -I --json

# Complete/Uncomplete
todo complete "Task" --json
todo complete 0 1 2 --json               # Batch by index
todo uncomplete "Task" --json

# Delete
todo rm "Task" -y --json
```

### Subtasks (Steps)

```bash
todo new-step "Task" "Step text" --json
todo list-steps "Task" --json
todo complete-step "Task" "Step" --json
todo uncomplete-step "Task" "Step" --json
todo rm-step "Task" 0 --json
```

### Notes

```bash
todo note "Task" "Note content"
todo show-note "Task"
todo clear-note "Task"
```

### Lists

```bash
todo lists --json
todo new-list "Project X" --json
todo rename-list "Old" "New" --json
todo rm-list "Project X" -y --json
```

## Task Identification

| Method           | Stability | Use Case            |
| ---------------- | --------- | ------------------- |
| `--id "AAMk..."` | Stable    | Automation, scripts |
| Index (`0`, `1`) | Unstable  | Interactive only    |
| Name (`"Task"`)  | Unstable  | Unique names only   |

Use ID for multi-step operations:

```bash
ID=$(todo new "Task" -l Work --json | jq -r '.id')
todo complete --id "$ID" -l Work --json
```

## Date & Time Formats

| Type     | Examples                            |
| -------- | ----------------------------------- |
| Relative | `1h`, `30m`, `2d`, `1h30m`          |
| Time     | `9:30`, `9am`, `17:00`, `5:30pm`    |
| Days     | `tomorrow`, `monday`, `fri`         |
| Date     | `2026-12-31`, `31.12.2026`          |
| Keywords | `morning` (7:00), `evening` (18:00) |

## Recurrence Patterns

| Pattern              | Description      |
| -------------------- | ---------------- |
| `daily`              | Every day        |
| `weekly`             | Every week       |
| `monthly`            | Every month      |
| `yearly`             | Every year       |
| `weekdays`           | Monday to Friday |
| `weekly:mon,wed,fri` | Specific days    |
| `every 2 days`       | Custom interval  |

## Aliases

| Alias | Command      |
| ----- | ------------ |
| `t`   | `tasks`      |
| `n`   | `new`        |
| `c`   | `complete`   |
| `d`   | `rm`         |
| `sn`  | `show-note`  |
| `cn`  | `clear-note` |

## Notes

- **Always use `--json`** for all commands to get structured output
- **Always use `-y`** with `rm` commands to skip confirmation
- Use `--id` with `-l ListName` for list context
- First run opens browser for OAuth authentication

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
