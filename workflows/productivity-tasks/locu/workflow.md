# locu

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/davidsmorais/locu/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/davidsmorais/locu/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Manage tasks and projects via Locu's Public API.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage tasks and projects via Locu's Public API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run locu`)
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
You are executing the locu workflow. Use the following context:

Description: Manage tasks and projects via Locu's Public API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: locu
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Locu Skill

Use the Locu Public API to interact with your workspace.

## Authentication
- `LOCU_API_TOKEN`: Your Personal Access Token (PAT).

## Commands

### User Info
- Get my info: `curl -X GET "https://api.locu.app/api/v1/me" -H "Authorization: Bearer $LOCU_API_TOKEN"`

### Tasks
- List tasks: `curl -X GET "https://api.locu.app/api/v1/tasks" -H "Authorization: Bearer $LOCU_API_TOKEN"`

### Projects
- List projects: `curl -X GET "https://api.locu.app/api/v1/projects" -H "Authorization: Bearer $LOCU_API_TOKEN"`

## Usage Notes
Always parse the JSON output to extract details about tasks (id, name, done status, type). Locu tasks can be native or integrated from Linear/Jira.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
