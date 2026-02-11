# mailbox

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/leeguooooo/mailbox/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/leeguooooo/mailbox/SKILL.md)
> Category: Communication

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
**Trigger:** User-invocable (via `aidarr run mailbox`)
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
You are executing the mailbox workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: mailbox
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Mailbox CLI (OpenClaw Skill)

Use the mailbox CLI as a tool to read and manage email. OpenClaw handles
channel delivery and scheduling. The mailbox CLI returns structured JSON
outputs and optional text summaries.

## Requirements
- mailbox CLI installed (`npm install -g mailbox-cli`)
- Credentials in `~/.config/mailbox/auth.json`

## Commands (examples)
- `mailbox account list --json`
- `mailbox email list --limit 20 --json`
- `mailbox email show <email_uid> --account-id <account_id> --json`
- `mailbox email show <email_uid> --account-id <account_id> --preview --no-html --json`
- `mailbox email show <email_uid> --account-id <account_id> --preview --no-html --strip-urls --json`
- `mailbox email delete <email_uid> --account-id <account_id> --folder INBOX --confirm --json`
- `mailbox digest run --json`
- `mailbox monitor run --json`
- `mailbox inbox --limit 15 --text`

## Safety rules
- Always use `--json` for automation and check `success`.
- Include `--account-id` for destructive operations.
- Destructive operations default to dry-run unless `--confirm` is provided.
- Prefer `--dry-run` before mutating when available.

## Output contract
- JSON response includes `success` and `error` fields.
- `error` is an object with `{ code, message, detail? }`.
- Exit codes: 0 success, 1 operation failed, 2 invalid usage.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
