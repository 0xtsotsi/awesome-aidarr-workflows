# kanbanflow-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/abakermi/kanbanflow-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/abakermi/kanbanflow-skill/SKILL.md)
> Category: Productivity & Tasks

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run kanbanflow-skill`)
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
You are executing the kanbanflow-skill workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: kanbanflow-skill
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

<skill>
  <name>kanbanflow</name>
  <description>Manage KanbanFlow board tasks (board, columns, tasks, add, move, color, delete). Use this to organize work and track progress.</description>
  <usage>
    <command>kanbanflow board</command>
    <command>kanbanflow columns</command>
    <command>kanbanflow tasks [columnId]</command>
    <command>kanbanflow add <columnId> <name> [description] [color]</command>
    <command>kanbanflow move <taskId> <columnId></command>
    <command>kanbanflow color <taskId> <color></command>
    <command>kanbanflow delete <taskId></command>
  </usage>
</skill>

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
