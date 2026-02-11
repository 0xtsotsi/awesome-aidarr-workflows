# openclaw-skill-blinko

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/vellis59/openclaw-skill-blinko/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/vellis59/openclaw-skill-blinko/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Manage Blinko notes via its REST API (create/list/delete notes, manage tags/taxonomy). Use when the user says “blinko …”, wants to capture a note to Blinko, list/search recent notes, retag notes, or do cleanup/organization. Requires BLINKO_API_KEY.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Blinko notes via its REST API (create/list/delete notes, manage tags/taxonomy). Use when the user says “blinko …”, wants to capture a note to Blinko, list/search recent notes, retag notes, or do cleanup/organization. Requires BLINKO_API_KEY.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run openclaw-skill-blinko`)
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
You are executing the openclaw-skill-blinko workflow. Use the following context:

Description: Manage Blinko notes via its REST API (create/list/delete notes, manage tags/taxonomy). Use when the user says “blinko …”, wants to capture a note to Blinko, list/search recent notes, retag notes, or do cleanup/organization. Requires BLINKO_API_KEY.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openclaw-skill-blinko
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Blinko

Use Blinko as the single source of truth for notes.

## Setup (one-time)

Env vars (Gateway env is OK):
- `BLINKO_API_KEY` (required)
- `BLINKO_BASE_URL` (optional; default `https://blinko.exemple.com`)

## Core workflow

### 1) Create a note
When user says something like:
- “blinko: …”
- “note: …”

Create a note with:
- Markdown body
- Add tags as hashtags at the end (respect the user’s taxonomy constraints)

### 2) List/search notes
If the user asks “liste mes notes” or “cherche …”, call the list endpoint and show:
- id
- first line/title
- top tags (if present)

### 3) Tagging rules (user constraints)
- Max **7** top-level tags.
- For each note: choose **1** top-level tag + **0–2** sub-tags max.
- Sub-tag syntax: `#Tech/dev`.

### 4) Destructive actions (delete/purge)
Always confirm explicitly ("OK vas-y") before:
- deleting notes
- deleting tags

Use the helper script for batch operations.

## Helper script

`scripts/blinko.py` wraps the API.

Examples:
```bash
# list
BLINKO_API_KEY=... ./scripts/blinko.py list --page 1 --size 20

# create
BLINKO_API_KEY=... ./scripts/blinko.py create --title "Test" --content "Hello" --tags "#Inbox #Todo/à-faire"

# delete (destructive)
BLINKO_API_KEY=... ./scripts/blinko.py delete --yes 123 124
```

## Reference

See `references/blinko_api.md` for endpoint cheat sheet.


## Github

https://github.com/Vellis59/openclaw-skill-blinko
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
