# notectl

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/rainbat/notectl/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/rainbat/notectl/SKILL.md)
> Category: Notes & PKM

---

## Description

Manage Apple Notes via AppleScript CLI

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Apple Notes via AppleScript CLI

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run notectl`)
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
You are executing the notectl workflow. Use the following context:

Description: Manage Apple Notes via AppleScript CLI

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: notectl
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# notectl - Apple Notes CLI

Manage Apple Notes from the command line using AppleScript.

## Commands

| Command | Description |
|---------|-------------|
| `notectl folders` | List all folders with note counts |
| `notectl list [folder]` | List notes in a folder (default: Notes) |
| `notectl show <title>` | Show note content by title |
| `notectl add <title>` | Create a new note |
| `notectl search <query>` | Search notes by title or content |
| `notectl append <title>` | Append text to an existing note |

## Examples

```bash
# List all folders
notectl folders

# List notes in default folder
notectl list

# List notes in specific folder
notectl list "rainbat-projects"
notectl list Papi

# Show a note
notectl show "Meeting Notes"

# Create a note
notectl add "New Idea"
notectl add "Project Plan" --folder research --body "Initial thoughts..."

# Search all notes
notectl search "clawdbot"
notectl search "API"

# Append to a note (daily log style)
notectl append "Daily Log" --text "- Completed feature X"
```

## Options for `add`

| Option | Description | Default |
|--------|-------------|---------|
| `-f, --folder <name>` | Folder to create note in | Notes |
| `-b, --body <text>` | Note body content | empty |

## Options for `append`

| Option | Description |
|--------|-------------|
| `-t, --text <text>` | Text to append to the note |

## Available Folders

Folders on this system:
- Notes (default)
- research
- rainbat-projects
- Papi
- renova-roll
- Journal
- CheatSheets
- pet-projects

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
