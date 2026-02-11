# tasktrove

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/willwebberley/tasktrove/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/willwebberley/tasktrove/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Manage todos via Tasktrove API. Use for listing, creating, completing, or updating tasks. Triggers on task/todo requests like "what's on my todo list", "add a task", "mark X done", "what's due today".

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage todos via Tasktrove API. Use for listing, creating, completing, or updating tasks. Triggers on task/todo requests like "what's on my todo list", "add a task", "mark X done", "what's due today".

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tasktrove`)
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
You are executing the tasktrove workflow. Use the following context:

Description: Manage todos via Tasktrove API. Use for listing, creating, completing, or updating tasks. Triggers on task/todo requests like "what's on my todo list", "add a task", "mark X done", "what's due today".

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tasktrove
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Tasktrove Todo Management

Manage tasks via a self-hosted [Tasktrove](https://tasktrove.io) instance. ([GitHub](https://github.com/dohsimpson/tasktrove))

## Configuration

Set the following environment variable:

```bash
export TASKTROVE_HOST="http://your-server:3333"
```

Optionally, if your instance requires authentication:
```bash
export TASKTROVE_TOKEN="your-api-token"
```

## Quick Reference

### Using the CLI script

```bash
# List today's tasks
python3 scripts/tasks.py list --today

# List overdue tasks
python3 scripts/tasks.py list --overdue

# List this week's tasks
python3 scripts/tasks.py list --week

# Add a task
python3 scripts/tasks.py add "Task title" --due 2026-02-10 --priority 2

# Complete a task (use ID prefix from list output)
python3 scripts/tasks.py complete abc123

# Search tasks
python3 scripts/tasks.py search "keyword"
```

### Direct API calls

#### List Tasks
```bash
curl -s "$TASKTROVE_HOST/api/v1/tasks"
```

#### Create Task
```bash
# Note: API requires all fields including id, completed, labels, etc.
curl -X POST "$TASKTROVE_HOST/api/v1/tasks" \
  -H "Content-Type: application/json" \
  -d '{
    "id": "<uuid>",
    "title": "Task title",
    "priority": 4,
    "dueDate": "2026-02-06",
    "completed": false,
    "labels": [],
    "subtasks": [],
    "comments": [],
    "createdAt": "2026-02-06T12:00:00.000Z",
    "recurringMode": "dueDate"
  }'
```

#### Complete/Update Task
```bash
# Note: PATCH goes to collection endpoint with ID in body (not /tasks/{id})
curl -X PATCH "$TASKTROVE_HOST/api/v1/tasks" \
  -H "Content-Type: application/json" \
  -d '{"id": "<task-id>", "completed": true}'
```

#### Delete Task
```bash
curl -X DELETE "$TASKTROVE_HOST/api/v1/tasks/<task-id>"
```

## Task Schema

| Field | Type | Notes |
|-------|------|-------|
| id | string | UUID (required on create) |
| title | string | Required |
| description | string | Optional |
| completed | boolean | Default false |
| priority | number | 1 (highest) to 4 (lowest) |
| dueDate | string | YYYY-MM-DD format |
| projectId | string | UUID of project |
| labels | string[] | Array of label UUIDs |
| subtasks | object[] | Nested subtasks |
| recurring | string | RRULE format |

## Priority Levels

- P1: Urgent/critical
- P2: High priority  
- P3: Medium priority
- P4: Low priority (default)

## Notes

- The Tasktrove UI supports natural language input, but the API expects structured JSON
- PATCH operations use the collection endpoint with ID in the request body
- POST requires all schema fields to be present

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
