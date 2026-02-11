# shared-memory

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/christinetyip/shared-memory/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/christinetyip/shared-memory/SKILL.md)
> Category: Notes & PKM

---

## Description

Share memories and state with other users. Use when user wants to share knowledge, create users/groups, grant permissions, set up family or team sharing, subscribe to memory changes, or manage access control on their memory knowledge base. This shared memory skill uses Ensue - a shared memory network for agents.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Share memories and state with other users. Use when user wants to share knowledge, create users/groups, grant permissions, set up family or team sharing, subscribe to memory changes, or manage access control on their memory knowledge base. This shared memory skill uses Ensue - a shared memory network for agents.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run shared-memory`)
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
You are executing the shared-memory workflow. Use the following context:

Description: Share memories and state with other users. Use when user wants to share knowledge, create users/groups, grant permissions, set up family or team sharing, subscribe to memory changes, or manage access control on their memory knowledge base. This shared memory skill uses Ensue - a shared memory network for agents.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: shared-memory
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Shared Memory

Share memories from your knowledge base with other users. Manage users, groups, and fine-grained permissions on namespaces.

## Quick Start

```bash
# Create user and group
{baseDir}/scripts/shared-memory.sh create-user mark
{baseDir}/scripts/shared-memory.sh create-group family
{baseDir}/scripts/shared-memory.sh add-member family mark

# Grant access
{baseDir}/scripts/shared-memory.sh grant group family read christine/shared/
{baseDir}/scripts/shared-memory.sh grant group family update christine/shared/
```

## Namespace Organization

```
<username>/
├── private/    # Only this user
├── shared/     # Shared with others
└── public/     # Read-only to others
```

Grant access to `mark/shared/` → all shared content
Grant access to `mark/shared/recipes/` → just recipes

## Commands

### Users
| Command | Description |
|---------|-------------|
| `create-user <username>` | Create user |
| `delete-user <username>` | Delete user |

### Groups
| Command | Description |
|---------|-------------|
| `create-group <name>` | Create group |
| `delete-group <name>` | Delete group |
| `add-member <group> <user>` | Add user to group |
| `remove-member <group> <user>` | Remove user |

### Permissions
| Command | Description |
|---------|-------------|
| `grant org <action> <pattern>` | Grant to org |
| `grant user <name> <action> <pattern>` | Grant to user |
| `grant group <name> <action> <pattern>` | Grant to group |
| `revoke <grant_id>` | Revoke permission |
| `list` | List all grants |
| `list-permissions` | List effective permissions |

**Actions**: `read`, `create`, `update`, `delete`

### Subscriptions
| Command | Description |
|---------|-------------|
| `subscribe <key>` | Get notified on changes |
| `unsubscribe <key>` | Stop notifications |
| `list-subscriptions` | List subscriptions |

## Example: Family Sharing

```bash
# Create user for partner
{baseDir}/scripts/shared-memory.sh create-user mark

# Create family group
{baseDir}/scripts/shared-memory.sh create-group family
{baseDir}/scripts/shared-memory.sh add-member family mark

# Grant mutual access to shared/ namespaces
{baseDir}/scripts/shared-memory.sh grant group family read christine/shared/
{baseDir}/scripts/shared-memory.sh grant group family create christine/shared/
{baseDir}/scripts/shared-memory.sh grant group family update christine/shared/
{baseDir}/scripts/shared-memory.sh grant group family read mark/shared/
{baseDir}/scripts/shared-memory.sh grant group family update mark/shared/
```

## Troubleshooting

If commands fail, first check if an Ensue API key is configured:

```bash
echo $ENSUE_API_KEY
grep -A2 'ensue-learning-memory' ~/.clawdbot/clawdbot.json
```

If no API key found, tell user to get a free key at https://www.ensue-network.ai/login and configure in `~/.clawdbot/clawdbot.json`:

```json
{
  "skills": {
    "entries": {
      "ensue-learning-memory": {
        "apiKey": "their-api-key-here"
      }
    }
  }
}
```

If key exists but commands fail, the key may be invalid - have user generate a new one.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
