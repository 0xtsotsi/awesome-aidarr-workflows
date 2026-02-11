# planka

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/voydz/planka/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/voydz/planka/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Manage Planka (Kanban) projects, boards, lists, cards, and notifications via a custom Python CLI.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Planka (Kanban) projects, boards, lists, cards, and notifications via a custom Python CLI.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run planka`)
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
You are executing the planka workflow. Use the following context:

Description: Manage Planka (Kanban) projects, boards, lists, cards, and notifications via a custom Python CLI.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: planka
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Planka CLI

This skill provides a CLI wrapper around the `plankapy` library to interact with a Planka instance.

## Setup

1.  **Install via Homebrew tap:**
    ```bash
    brew tap voydz/homebrew-tap
    brew install planka-cli
    ```

    Source/pipx installs require Python 3.11+ to use plankapy v2.

2.  **Configuration:**
    Use the `login` command to store credentials:
    ```bash
    planka-cli login --url https://planka.example --username alice --password secret
    # or: python3 scripts/planka_cli.py login --url https://planka.example --username alice --password secret
    ```

## Usage

Run the CLI with the installed `planka-cli` binary:

```bash
# Show help
planka-cli

# Check connection
planka-cli status

# Login to planka instance
planka-cli login --url https://planka.example --username alice --password secret

# Remove stored credentials
planka-cli logout

# List Projects
planka-cli projects list

# List Boards (optionally by project ID)
planka-cli boards list [PROJECT_ID]

# List Lists in a Board
planka-cli lists list <BOARD_ID>

# List Cards in a List
planka-cli cards list <LIST_ID>

# Show a Card (includes attachments with URLs and comment text)
planka-cli cards show <CARD_ID>

# Create a Card
planka-cli cards create <LIST_ID> "Card title"

# Update a Card
planka-cli cards update <CARD_ID> --name "New title"
planka-cli cards update <CARD_ID> --list-id <LIST_ID>
planka-cli cards update <CARD_ID> --list-id <LIST_ID> --position top

# Delete a Card
planka-cli cards delete <CARD_ID>

# Notifications
planka-cli notifications all
planka-cli notifications unread
```

## Examples

**List all boards:**
```bash
planka-cli boards list
```

**Show cards in list ID 1619901252164912136:**
```bash
planka-cli cards list 1619901252164912136
```

**Show card details for card ID 1619901252164912137:**
```bash
planka-cli cards show 1619901252164912137
```

**Create a card in list ID 1619901252164912136:**
```bash
planka-cli cards create 1619901252164912136 "Ship CLI"
```

**Move a card to another list:**
```bash
planka-cli cards update 1619901252164912137 --list-id 1619901252164912136
```

**Move a card to another list and pin it to the top:**
```bash
planka-cli cards update 1619901252164912137 --list-id 1619901252164912136 --position top
```

**Mark a card done by updating its name:**
```bash
planka-cli cards update 1619901252164912137 --name "Done: Ship CLI"
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
