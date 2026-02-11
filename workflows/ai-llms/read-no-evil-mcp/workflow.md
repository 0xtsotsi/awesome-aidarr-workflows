# read-no-evil-mcp

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/thekie/read-no-evil-mcp/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/thekie/read-no-evil-mcp/SKILL.md)
> Category: AI & LLMs

---

## Description

Secure email access via read-no-evil-mcp. Protects against prompt injection attacks in emails. Use for reading, sending, deleting, and moving emails.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Secure email access via read-no-evil-mcp. Protects against prompt injection attacks in emails. Use for reading, sending, deleting, and moving emails.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run read-no-evil-mcp`)
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
You are executing the read-no-evil-mcp workflow. Use the following context:

Description: Secure email access via read-no-evil-mcp. Protects against prompt injection attacks in emails. Use for reading, sending, deleting, and moving emails.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: read-no-evil-mcp
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# read-no-evil-mcp

Secure email gateway that scans emails for prompt injection attacks before you see them.

## Prerequisites

Install the read-no-evil-mcp package (version must match skill version):

```bash
pip install read-no-evil-mcp==0.2.0
```

## Configuration

### Config File

Create `~/.config/read-no-evil-mcp/config.yaml`:

```yaml
accounts:
  - id: "default"
    type: "imap"
    host: "mail.example.com"
    port: 993
    username: "you@example.com"
    ssl: true
    permissions:
      read: true
      send: false
      delete: false
      move: false
    smtp_host: "mail.example.com"
    smtp_port: 587
    from_address: "you@example.com"
    from_name: "Your Name"
```

### Credentials

Create `~/.config/read-no-evil-mcp/.env`:

```bash
RNOE_ACCOUNT_DEFAULT_PASSWORD=your-password
```

Environment variable format: `RNOE_ACCOUNT_{ACCOUNT_ID}_PASSWORD` (uppercase).

## CLI Commands

```bash
# List recent emails (last 30 days)
rnoe-mail.py list

# List with options
rnoe-mail.py list --limit 10 --days 7 --account myaccount

# Read email (scanned for prompt injection!)
rnoe-mail.py read <uid>

# Send email (requires send permission)
rnoe-mail.py send --to "user@example.com" --subject "Hello" --body "Message"

# List folders
rnoe-mail.py folders

# Move email to folder
rnoe-mail.py move <uid> --to "Archive"
```

## Prompt Injection Detection

All emails are automatically scanned:

- **Safe**: Content displayed normally
- **Injection detected**: Exit code 2, shows score + patterns

Uses ProtectAI's DeBERTa model (local inference, no external APIs).

## Permissions

| Permission | Description | Default |
|------------|-------------|---------|
| `read` | List and read emails | `true` |
| `send` | Send emails via SMTP | `false` |
| `delete` | Delete emails | `false` |
| `move` | Move emails between folders | `false` |

## Security Notes

- Emails are scanned for prompt injection before content is returned
- ML model runs locally — no data sent to external APIs
- Enable write permissions only when needed
- Consider using app-specific passwords

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
