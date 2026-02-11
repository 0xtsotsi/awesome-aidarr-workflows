# workflowy

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/waldyrious/workflowy/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/waldyrious/workflowy/SKILL.md)
> Category: Browser & Automation

---

## Description

Workflowy outliner CLI for reading, searching, and editing nodes. Use when the user wants to interact with their Workflowy outline — searching, adding items, viewing trees, marking complete, bulk operations, or usage reports.

**Homepage:** https://github.com/mholzen/workflowy
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Workflowy outliner CLI for reading, searching, and editing nodes. Use when the user wants to interact with their Workflowy outline — searching, adding items, viewing trees, marking complete, bulk operations, or usage reports.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run workflowy`)
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
You are executing the workflowy workflow. Use the following context:

Description: Workflowy outliner CLI for reading, searching, and editing nodes. Use when the user wants to interact with their Workflowy outline — searching, adding items, viewing trees, marking complete, bulk operations, or usage reports.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: workflowy
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: https://github.com/mholzen/workflowy
```

---

## Original Skill Content



# workflowy

Use the unofficial `workflowy` CLI [mholzen/workflowy](https://github.com/mholzen/workflowy) for managing a Workflowy outline. Requires API key setup.

## Setup (once)

Get your API key at https://workflowy.com/api-key/, and save it to `~/.workflowy/api.key`:

```bash
mkdir -p ~/.workflowy
echo "your-api-key-here" > ~/.workflowy/api.key
```

## Common commands

### Reading

```bash
# Get root nodes (depth 2 by default)
workflowy get

# Get specific node by UUID or short ID
workflowy get <item-id>
workflowy get https://workflowy.com/#/59fc7acbc68c

# Show a node's children as a flat list
workflowy list <item-id>

# Search (full text, case-insensitive)
workflowy search -i "meeting notes"

# Search with extended regex
workflowy search -E "<time.*>"

# Search within a subtree
workflowy search "bug" --item-id <parent-id>
```

### Writing

```bash
# Add a new node to the Inbox
workflowy create "Buy groceries" --parent-id=inbox

# Add a node to a specific parent
workflowy create "Task" --parent-id=<uuid>

# Update a node
workflowy update <item-id> --name "New name"

# Complete/uncomplete
workflowy complete <item-id>
workflowy uncomplete <item-id>

# Move a node
workflowy move <item-id> <new-parent-id>

# Delete a node (includes its children!)
workflowy delete <item-id>
```

### Bulk operations

```bash
# Search and replace (dry run first!)
workflowy replace --dry-run "foo" "bar"
workflowy replace --interactive "foo" "bar"

# Regex find/replace using capture groups
workflowy replace "TASK-([0-9]+)" 'ISSUE-$1'

# Transform: split by newlines into children
workflowy transform <item-id> split -s "\n"

# Transform: trim whitespace
workflowy transform <item-id> trim
```

### Statistics

```bash
# Where is most content?
workflowy report count --threshold 0.01

# Nodes with most children
workflowy report children --top-n 20

# Stale content (oldest modified)
workflowy report modified --top-n 50

# Most mirrored nodes (requires backup)
workflowy report mirrors --top-n 20
```

## Data Access Methods

| Method            | Speed         | Freshness | Use For           |
|-------------------|---------------|-----------|-------------------|
| `--method=get`    | Medium        | Real-time | Specific items    |
| `--method=export` | Fast (cached) | ~1 min    | Full tree access  |
| `--method=backup` | Fastest       | Stale     | Bulk ops, offline |

For offline mode, enable Workflowy's Dropbox backup:
```bash
workflowy get --method=backup
```

## Short IDs

Workflowy supports short IDs, obtained from the "Copy Internal Link" menu:
- Web URL: `https://workflowy.com/#/59fc7acbc68c`
- Can be used directly, e.g. `workflowy get https://workflowy.com/#/59fc7acbc68c`

## Special named targets

- `inbox` — user's inbox
- `home` — root of outline

```bash
workflowy create "Quick note" --parent-id=inbox
workflowy id inbox  # resolve to UUID
```

## Notes

- Deleting a node also deletes all its children
- Results are sorted by priority (display order)
- Use `--method=export` for large tree operations (cached, faster)
- Mirror analysis requires using the backup method
- Make sure to confirm before performing bulk replace operations

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
