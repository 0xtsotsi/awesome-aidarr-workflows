# vikunja

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dbhurley/vikunja/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dbhurley/vikunja/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Manage projects and tasks in Vikunja, an open-source project management tool. Create projects, tasks, set due dates, priorities, and track completion.

**Homepage:** https://vikunja.io
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage projects and tasks in Vikunja, an open-source project management tool. Create projects, tasks, set due dates, priorities, and track completion.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run vikunja`)
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
You are executing the vikunja workflow. Use the following context:

Description: Manage projects and tasks in Vikunja, an open-source project management tool. Create projects, tasks, set due dates, priorities, and track completion.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: vikunja
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: https://vikunja.io
```

---

## Original Skill Content



# Vikunja Project Management

Manage projects and tasks in [Vikunja](https://vikunja.io), an open-source, self-hosted project management tool.

## Setup

Set these environment variables:
- `VIKUNJA_URL` - Your Vikunja instance URL (e.g., `https://vikunja.example.com`)
- `VIKUNJA_USER` - Username or email
- `VIKUNJA_PASSWORD` - Password

## Commands

### Projects
```bash
# List all projects
uv run {baseDir}/scripts/vikunja.py projects

# Get project details
uv run {baseDir}/scripts/vikunja.py project <ID>

# Create a project
uv run {baseDir}/scripts/vikunja.py create-project "Project Name" -d "Description"
```

### Tasks
```bash
# List all tasks
uv run {baseDir}/scripts/vikunja.py tasks

# List tasks in a specific project
uv run {baseDir}/scripts/vikunja.py tasks --project <PROJECT_ID>

# Create a task
uv run {baseDir}/scripts/vikunja.py create-task "Task title" --project <ID> --due 2026-01-15 --priority 3

# Mark task complete
uv run {baseDir}/scripts/vikunja.py complete <TASK_ID>
```

### Options
- `--json` - Output results as JSON (for programmatic use)

## Priority Levels
- 0: None
- 1: Low
- 2: Medium  
- 3: High
- 4: Urgent
- 5: Critical

## Examples

```bash
# Create a project for Q1 planning
uv run {baseDir}/scripts/vikunja.py create-project "Q1 2026 Planning" -d "Quarterly planning tasks"

# Add a high-priority task
uv run {baseDir}/scripts/vikunja.py create-task "Review budget" --project 5 --due 2026-01-20 --priority 3

# Check what's due
uv run {baseDir}/scripts/vikunja.py tasks --project 5 --json
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
