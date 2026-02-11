# mailgun

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/alphafactor/mailgun/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/alphafactor/mailgun/SKILL.md)
> Category: Communication

---

## Description

Send emails via Mailgun API. Use when the user needs to send emails programmatically, such as newsletters, notifications, alerts, or automated reports. Requires MAILGUN_API_KEY and MAILGUN_DOMAIN environment variables to be configured.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Send emails via Mailgun API. Use when the user needs to send emails programmatically, such as newsletters, notifications, alerts, or automated reports. Requires MAILGUN_API_KEY and MAILGUN_DOMAIN environment variables to be configured.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run mailgun`)
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
You are executing the mailgun workflow. Use the following context:

Description: Send emails via Mailgun API. Use when the user needs to send emails programmatically, such as newsletters, notifications, alerts, or automated reports. Requires MAILGUN_API_KEY and MAILGUN_DOMAIN environment variables to be configured.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: mailgun
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Mailgun Email Sender

Send emails programmatically using Mailgun's HTTP API.

## Prerequisites

Configure the following environment variables in `~/.zshrc` or `~/.bash_profile`:

```bash
export MAILGUN_API_KEY="key-xxxxx"      # Your Mailgun private API key
export MAILGUN_DOMAIN="mg.yourdomain.com"  # Your Mailgun domain
export MAILGUN_FROM="Sender <noreply@mg.yourdomain.com>"  # Default sender
export MAILGUN_DEFAULT_TO="you@email.com"  # Default recipient (optional)
```

Then reload your shell configuration:
```bash
source ~/.zshrc
```

## Usage

### Send a simple email

```bash
mailgun/scripts/send_email.sh "Subject" "Email body text"
```

### Send to a specific recipient

```bash
mailgun/scripts/send_email.sh "Newsletter" "Content here" "recipient@email.com"
```

### Send with custom sender

```bash
mailgun/scripts/send_email.sh "Alert" "System down" "admin@company.com" "alerts@company.com"
```

## Features

- Simple command-line interface
- Uses environment variables for configuration
- Supports custom sender and recipient
- Returns success/error status codes
- Works with HTML content (pass HTML in body parameter)

## Common Use Cases

- Daily/weekly newsletters
- System alerts and notifications
- Automated reports
- Confirmation emails
- Scheduled reminders

## Troubleshooting

**Error: MAILGUN_API_KEY and MAILGUN_DOMAIN must be set**
→ Configure environment variables as shown in Prerequisites

**Error: 401 Unauthorized**
→ Check that your API key is correct and active

**Error: 404 Not Found**
→ Verify your MAILGUN_DOMAIN is correct

## References

- Mailgun Documentation: https://documentation.mailgun.com/
- API Reference: See [references/api.md](references/api.md)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
