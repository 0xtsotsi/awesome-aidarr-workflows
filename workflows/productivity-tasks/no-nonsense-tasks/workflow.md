# no-nonsense-tasks

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dvjn/no-nonsense-tasks/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dvjn/no-nonsense-tasks/SKILL.md)
> Category: Productivity & Tasks

---

## Description

No-nonsense task manager using SQLite. Track tasks with statuses (backlog, todo, in-progress, done), descriptions, and tags. Use when managing personal tasks, to-do items, project tracking, or any workflow that needs status-based task organization. Supports adding, listing, filtering, updating, moving, and deleting tasks.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
No-nonsense task manager using SQLite. Track tasks with statuses (backlog, todo, in-progress, done), descriptions, and tags. Use when managing personal tasks, to-do items, project tracking, or any workflow that needs status-based task organization. Supports adding, listing, filtering, updating, moving, and deleting tasks.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run no-nonsense-tasks`)
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
You are executing the no-nonsense-tasks workflow. Use the following context:

Description: No-nonsense task manager using SQLite. Track tasks with statuses (backlog, todo, in-progress, done), descriptions, and tags. Use when managing personal tasks, to-do items, project tracking, or any workflow that needs status-based task organization. Supports adding, listing, filtering, updating, moving, and deleting tasks.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: no-nonsense-tasks
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# No Nonsense Tasks

Simple SQLite-backed task tracking. No fluff, no complexity, just tasks that get done.

## Prerequisites

- `sqlite3` CLI tool must be installed

## Quick Start

Initialize the database:

```bash
./scripts/init_db.sh
```

Add your first task:

```bash
./scripts/task_add.sh "Build task tracker skill" \
  --description "Create a SQLite-based task manager" \
  --tags "work,urgent" \
  --status todo
```

List all tasks:

```bash
./scripts/task_list.sh
```

## Task Statuses

Tasks flow through four statuses:

- **backlog** - Ideas and future tasks
- **todo** - Ready to work on
- **in-progress** - Currently being worked on
- **done** - Completed tasks

## Commands

### Initialize Database

```bash
./scripts/init_db.sh
```

Default location: `~/.no-nonsense/tasks.db`  
Override with: `export NO_NONSENSE_TASKS_DB=/path/to/tasks.db`

### Add Task

```bash
./scripts/task_add.sh <title> [options]
```

**Options:**
- `-d, --description TEXT` - Task description
- `-t, --tags TAGS` - Comma-separated tags
- `-s, --status STATUS` - Task status (default: backlog)

**Example:**
```bash
./scripts/task_add.sh "Deploy to prod" --description "Deploy v2.0" --tags "deploy,critical" --status todo
```

### List Tasks

```bash
./scripts/task_list.sh [--status STATUS]
```

**Examples:**
```bash
./scripts/task_list.sh              # All tasks
./scripts/task_list.sh --status todo
```

### Show Task Details

```bash
./scripts/task_show.sh <task_id>
```

### Move Task to Different Status

```bash
./scripts/task_move.sh <task_id> --status <STATUS>
```

**Example:**
```bash
./scripts/task_move.sh 7 --status in-progress
```

### Update Task Fields

```bash
./scripts/task_update.sh <task_id> [options]
```

**Options:**
- `--title TEXT` - Update title
- `-d, --description TEXT` - Update description
- `-t, --tags TAGS` - Update tags (comma-separated)
- `-s, --status STATUS` - Update status

### Update Tags (Shortcut)

```bash
./scripts/task_tag.sh <task_id> --tags <TAGS>
```

**Example:**
```bash
./scripts/task_tag.sh 8 --tags "urgent,bug,frontend"
```

### Filter by Tag

```bash
./scripts/task_filter.sh <tag>
```

### Delete Task

```bash
./scripts/task_delete.sh <task_id>
```

### View Statistics

```bash
./scripts/task_stats.sh
```

Shows count of tasks by status and total.

## Usage Tips

**Typical workflow:**

1. Add new ideas to backlog: `task_add.sh "Task idea" --status backlog`
2. Move tasks to todo when ready: `task_move.sh <id> --status todo`
3. Start work: `task_move.sh <id> --status in-progress`
4. Complete: `task_move.sh <id> --status done`

**Tag organization:**

- Use tags for categories: `work`, `personal`, `urgent`, `bug`, `feature`
- Combine tags: `urgent,work,api` or `personal,home,shopping`
- Filter by any tag: `task_filter.sh urgent`

**Status filtering:**

- Focus on current work: `task_list.sh --status in-progress`
- Plan your day: `task_list.sh --status todo`
- Review completed: `task_list.sh --status done`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
