# resend

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mjrussell/resend/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mjrussell/resend/SKILL.md)
> Category: Notes & PKM

---

## Description

Manage received (inbound) emails and attachments via Resend API. Use when user asks about their emails, received messages, or email attachments.

**Homepage:** https://resend.com
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage received (inbound) emails and attachments via Resend API. Use when user asks about their emails, received messages, or email attachments.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run resend`)
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
You are executing the resend workflow. Use the following context:

Description: Manage received (inbound) emails and attachments via Resend API. Use when user asks about their emails, received messages, or email attachments.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: resend
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: https://resend.com
```

---

## Original Skill Content



# Resend CLI

CLI for the Resend email API. Query received (inbound) emails and attachments.

## Installation

```bash
npm install -g @mjrussell/resend-cli
```

## Setup

1. Sign up at [resend.com](https://resend.com)
2. Set up inbound email routing for your domain
3. Create API key at API Keys → Create API key (needs read permissions)
4. Set environment variable: `export RESEND_API_KEY="re_your_key"`

## Commands

### List Emails

```bash
resend email list              # List recent emails (default 10)
resend email list -l 20        # List 20 emails
resend email list --json       # Output as JSON
```

### Get Email Details

```bash
resend email get <id>          # Show email details
resend email get <id> --json   # Output as JSON
```

### Attachments

```bash
resend email attachments <email_id>                    # List attachments
resend email attachment <email_id> <attachment_id>     # Get attachment metadata
resend email attachments <email_id> --json             # Output as JSON
```

### Domains

```bash
resend domain list             # List configured domains
resend domain get <id>         # Get domain details with DNS records
resend domain list --json      # Output as JSON
```

## Usage Examples

**User: "Do I have any new emails?"**
```bash
resend email list -l 5
```

**User: "Show me the latest email"**
```bash
resend email list --json | jq -r '.data.data[0].id'  # Get ID
resend email get <id>
```

**User: "What attachments are on that email?"**
```bash
resend email attachments <email_id>
```

**User: "What domains do I have set up?"**
```bash
resend domain list
```

**User: "Show me the full content of email X"**
```bash
resend email get <email_id>
```

## Notes

- This CLI only supports **received (inbound)** emails, not sending
- Use `--json` flag and pipe to `jq` for scripting
- Email IDs are UUIDs shown in list output

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
