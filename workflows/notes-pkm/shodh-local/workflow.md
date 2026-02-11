# shodh-local

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/doobidoo/shodh-local/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/doobidoo/shodh-local/SKILL.md)
> Category: Notes & PKM

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
**Trigger:** User-invocable (via `aidarr run shodh-local`)
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
You are executing the shodh-local workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: shodh-local
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Shodh-Local (v0.1.74)

Local-first brain for OpenClaw. Offline, learns with use.

## Config (TOOLS.md)
- **Binary**: `./shodh-memory-server` (or add to PATH)
- **Server**: `localhost:3030`
- **Data**: `./shodh-data`
- **Key**: `<YOUR-API-KEY>` (X-API-Key, generate via shodh-memory-server)
- **Manage**: `process` tool (session `amber-seaslug`)
- **TUI**: `cd tools/shodh-memory && ./shodh-tui` (graph/activity)

## Quick Use
```
KEY='<YOUR-API-KEY>'
curl -s -X POST http://localhost:3030/api/remember \\
-H &quot;Content-Type: application/json&quot; -H &quot;X-API-Key: $KEY&quot; \\
-d &#39;{&quot;user_id&quot;: &quot;henry&quot;, &quot;content&quot;: &quot;Test memory&quot;, &quot;memory_type&quot;: &quot;Learning&quot;, &quot;tags&quot;: [&quot;test&quot;]}&#39;
```

## Core Tools
- **Remember**: `/api/remember` (types: Learning/Observation/Conversation/Task/Preference)
- **Recall**: `/api/recall` (semantic) | `/api/recall/tags`
- **Proactive**: `/api/proactive_context` (auto-relevant)
- **Todos**: `/api/todos/add` | `/api/todos` | `/api/todos/complete`
- **Projects**: `/api/projects/add` | `/api/projects`
- **Summary**: `/api/context_summary`

Full API: [reference/api.md](reference/api.md)

## Best Practices
- **User ID**: `henry` (main), `openclaw` (system), `task-XYZ` (sub-agents)
- **Tags**: Always add for filtering (e.g. [&quot;openclaw&quot;, &quot;project-backend&quot;])
- **Before reply**: Recall recent context for continuity
- **Heartbeat**: Check todos daily
- **Maintenance**: Restart server weekly (`process kill amber-seaslug` + restart)

Read [reference/examples.md](reference/examples.md) for OpenClaw patterns.
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
