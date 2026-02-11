# notesctl-skill-for-openclaw

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/clinchcc/notesctl-skill-for-openclaw/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/clinchcc/notesctl-skill-for-openclaw/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Manage Apple Notes via deterministic local scripts (create, append, list, search, export, and edit). Use when a user asks OpenClaw to add a note, list notes, search notes, or manage note folders.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Apple Notes via deterministic local scripts (create, append, list, search, export, and edit). Use when a user asks OpenClaw to add a note, list notes, search notes, or manage note folders.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run notesctl-skill-for-openclaw`)
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
You are executing the notesctl-skill-for-openclaw workflow. Use the following context:

Description: Manage Apple Notes via deterministic local scripts (create, append, list, search, export, and edit). Use when a user asks OpenClaw to add a note, list notes, search notes, or manage note folders.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: notesctl-skill-for-openclaw
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# notesctl (Apple Notes, low-token)

## Goal

Minimize token usage and avoid fragile quoting by routing Apple Notes operations through bundled scripts.

## Quick start

### Create a new note (deterministic title/body)

- JSON stdin (recommended):

```bash
echo '{"title":"Title","body":"Line 1\nLine 2","folder":"Notes"}' | {baseDir}/scripts/notes_post.sh
```

- Direct args:

```bash
{baseDir}/scripts/notes_new.sh "Title" $'Body line 1\nBody line 2' "Notes"
```

### List/search/export

```bash
{baseDir}/scripts/notes_list.sh "Notes"
{baseDir}/scripts/notes_search.sh "query" "Notes"
{baseDir}/scripts/notes_export.sh "query" "Notes" "/tmp"  # interactive select then export
```

## Output conventions

- Keep receipts short: `Wrote to Notes: <title>`. 

## Notes on editing

Editing existing notes is inherently more fragile:
- Prefer append workflows or create a new note with a reference.
- If the user explicitly wants interactive editing, use `memo notes -e` (manual selection + editor).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
