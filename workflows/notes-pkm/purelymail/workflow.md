# purelymail

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dbhurley/purelymail/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dbhurley/purelymail/SKILL.md)
> Category: Notes & PKM

---

## Description

Set up and test PurelyMail email for Clawdbot agents. Generate configs, test IMAP/SMTP, verify inbox connectivity.

**Homepage:** https://purelymail.com
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Set up and test PurelyMail email for Clawdbot agents. Generate configs, test IMAP/SMTP, verify inbox connectivity.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run purelymail`)
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
You are executing the purelymail workflow. Use the following context:

Description: Set up and test PurelyMail email for Clawdbot agents. Generate configs, test IMAP/SMTP, verify inbox connectivity.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: purelymail
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: https://purelymail.com
```

---

## Original Skill Content



# PurelyMail Setup for Clawdbot

Set up email for your Clawdbot agent using [PurelyMail](https://purelymail.com) - a simple, privacy-focused email service perfect for agent inboxes.

## Why PurelyMail?

- **Cheap**: ~$10/year for unlimited addresses
- **Simple**: No bloat, just email
- **Privacy**: Based in US, minimal data retention
- **Reliable**: Great deliverability
- **Agent-friendly**: Easy IMAP/SMTP setup

## Quick Start (Wizard)

The easiest way to set up is with the interactive wizard:

```bash
purelymail wizard
```

The wizard will:
1. ✓ Check if you have a PurelyMail account
2. ✓ Test your IMAP/SMTP connection
3. ✓ Generate clawdbot.json config
4. ✓ Optionally send a test email

## Manual Setup

### 1. Create PurelyMail Account

1. Go to [purelymail.com](https://purelymail.com) and sign up
2. Add your domain (or use their subdomain)
3. Create a mailbox for your agent (e.g., `agent@yourdomain.com`)
4. Note the password

### 2. Generate Clawdbot Config

```bash
purelymail config --email agent@yourdomain.com --password "YourPassword"
```

Outputs JSON to add to your `clawdbot.json`:

```json
{
  "skills": {
    "entries": {
      "agent-email": {
        "env": {
          "AGENT_EMAIL": "agent@yourdomain.com",
          "AGENT_EMAIL_PASSWORD": "YourPassword",
          "AGENT_IMAP_SERVER": "imap.purelymail.com",
          "AGENT_SMTP_SERVER": "smtp.purelymail.com"
        }
      }
    }
  }
}
```

### 3. Test Connection

```bash
purelymail test --email agent@yourdomain.com --password "YourPassword"
```

Tests IMAP and SMTP connectivity.

### 4. Send Test Email

```bash
purelymail send-test --email agent@yourdomain.com --password "YourPassword" --to you@example.com
```

### 5. Check Inbox

```bash
purelymail inbox --email agent@yourdomain.com --password "YourPassword" --limit 5
```

## Commands

| Command | Description |
|---------|-------------|
| `config` | Generate clawdbot.json config snippet |
| `test` | Test IMAP/SMTP connectivity |
| `send-test` | Send a test email |
| `inbox` | List recent inbox messages |
| `read` | Read a specific email |
| `setup-guide` | Print full setup instructions |

## Environment Variables

Once configured in clawdbot.json, these env vars are available:

- `AGENT_EMAIL` - The email address
- `AGENT_EMAIL_PASSWORD` - The password
- `AGENT_IMAP_SERVER` - IMAP server (imap.purelymail.com)
- `AGENT_SMTP_SERVER` - SMTP server (smtp.purelymail.com)

## PurelyMail Settings

| Setting | Value |
|---------|-------|
| IMAP Server | `imap.purelymail.com` |
| IMAP Port | `993` (SSL) |
| SMTP Server | `smtp.purelymail.com` |
| SMTP Port | `465` (SSL) or `587` (STARTTLS) |
| Auth | Email + Password |

## Tips

- Use a strong, unique password for your agent
- Consider creating a dedicated domain for agent emails
- PurelyMail supports catch-all addresses (great for routing)
- Enable 2FA on your PurelyMail account (use app password for agent)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
