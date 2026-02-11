# cognary-ai-tasks

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dboyne/cognary-ai-tasks/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dboyne/cognary-ai-tasks/SKILL.md)
> Category: AI & LLMs

---

## Description

Manage task lists via cognary-cli. Use for listing, adding, updating, completing, uncompleting, and deleting tasks. Triggers on any request about tasks, to-dos, task lists, reminders-as-tasks, or tracking action items.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage task lists via cognary-cli. Use for listing, adding, updating, completing, uncompleting, and deleting tasks. Triggers on any request about tasks, to-dos, task lists, reminders-as-tasks, or tracking action items.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run cognary-ai-tasks`)
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
You are executing the cognary-ai-tasks workflow. Use the following context:

Description: Manage task lists via cognary-cli. Use for listing, adding, updating, completing, uncompleting, and deleting tasks. Triggers on any request about tasks, to-dos, task lists, reminders-as-tasks, or tracking action items.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: cognary-ai-tasks
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Cognary Tasks

Manage tasks via `cognary-cli tasks`. Always pass `--json` for parseable output.

## Installation

If `cognary-cli` is not installed, install it first:

```bash
npm install -g cognary-cli
```

## Auth

The `COGNARY_API_KEY` env var must be set. If calls fail with an auth error, tell the user:

- If they don't have an account or API key, they can register at **https://tasks.cognary.ai**
- Once in the app, go to the **Settings** menu and select **"MANAGE API KEYS"** to create a new key
- Then provide the key so it can be configured

## Commands

### List tasks

```bash
cognary-cli tasks list [--status active|completed|all] [--category <cat>] [--priority High|Medium|Low] [--search <query>] [--sort createdAt|updatedAt|dueDate|priority|title] [--order asc|desc] [--limit <n>] [--page <n>] [--active-only] [--completed-limit <n>] --json
```

Default: all tasks, sorted by createdAt desc, limit 20.

### Add task

```bash
cognary-cli tasks add "<title>" [--notes "<notes>"] [--category "<cat>"] [--priority High|Medium|Low] [--due-date "<date>"] --json
```

### Get task

```bash
cognary-cli tasks get <id> --json
```

### Update task

```bash
cognary-cli tasks update <id> [--title "<title>"] [--notes "<notes>"] [--category "<cat>"] [--priority High|Medium|Low] [--due-date "<date>"] --json
```

### Complete task

```bash
cognary-cli tasks complete <id> --json
```

### Uncomplete task (reactivate)

```bash
cognary-cli tasks uncomplete <id> --json
```

### Delete task

```bash
cognary-cli tasks delete <id> --json
```

## Formatting

- When listing tasks, present them in a clean readable format (not raw JSON).
- Show: title, status, priority, category, due date (if set), and ID.
- Group active vs completed when showing all.
- Use emoji for priority: 🔴 High, 🟡 Medium, 🟢 Low.
- When confirming actions (add/complete/delete), be brief.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
