# send-email

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/fontstep/send-email/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/fontstep/send-email/SKILL.md)
> Category: Communication

---

## Description

Send emails via SMTP. Configure in ~/.openclaw/openclaw.json under skills.entries.send-email.env.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Send emails via SMTP. Configure in ~/.openclaw/openclaw.json under skills.entries.send-email.env.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run send-email`)
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
You are executing the send-email workflow. Use the following context:

Description: Send emails via SMTP. Configure in ~/.openclaw/openclaw.json under skills.entries.send-email.env.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: send-email
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Send Email

Send emails via the Python script. SMTP settings are **injected by OpenClaw at runtime** when the script runs (from `~/.openclaw/openclaw.json` → `skills.entries.send-email.env`). **Do not read** any config file (e.g. `~/.openclaw/openclaw.json` or `workspace/openclaw.json`) — that would expose credentials in tool output. Just run the script; env is injected automatically. Do not use ~/.msmtprc.

## Configuration

Configure in **`~/.openclaw/openclaw.json`**:

```json
"skills": {
  "entries": {
    "send-email": {
      "enabled": true,
      "env": {
        "EMAIL_SMTP_SERVER": "smtp.163.com",
        "EMAIL_SMTP_PORT": "465",
        "EMAIL_SENDER": "your-email@163.com",
        "EMAIL_SMTP_PASSWORD": "YOUR_AUTH_CODE"
      }
    }
  }
}
```

| Variable | Description |
|----------|-------------|
| EMAIL_SMTP_SERVER | SMTP server, e.g. smtp.163.com, smtp.gmail.com |
| EMAIL_SMTP_PORT | Port, 465 (SSL) or 587 (TLS) |
| EMAIL_SENDER | Sender email address |
| EMAIL_SMTP_PASSWORD | Authorization code / app password (163/QQ: auth code; Gmail: App Password) |

## Agent instructions

1. **Credentials**: Never read config files. OpenClaw injects `skills.entries.send-email.env` when the script runs — do not use the read tool on `~/.openclaw/openclaw.json` or `workspace/openclaw.json` (exposes secrets). If the skill is enabled, assume env is configured; do not ask the user for passwords. Do not use ~/.msmtprc.
2. **Send mail**: Run the script under **workspace** (do not use the path under node_modules):
   ```bash
   python3 ~/.openclaw/workspace/skills/send-email/send_email.py "recipient" "Subject" "Body"
   ```
3. **Attachment**: `python3 ~/.openclaw/workspace/skills/send-email/send_email.py "recipient" "Subject" "Body" "/path/to/file.pdf"`

## Usage examples

```bash
python3 ~/.openclaw/workspace/skills/send-email/send_email.py 'recipient@example.com' 'Subject' 'Body text'
python3 ~/.openclaw/workspace/skills/send-email/send_email.py 'recipient@example.com' 'Subject' 'Body' '/path/to/file.pdf'
```

## SMTP reference

- 163: `smtp.163.com:465`, requires authorization code (not login password)
- Gmail: `smtp.gmail.com:587`, requires App Password
- QQ: `smtp.qq.com:465`, requires authorization code

## Troubleshooting

- Authentication failed: Check that `EMAIL_SMTP_PASSWORD` is the authorization code or App Password.
- Connection failed: Check `EMAIL_SMTP_SERVER` and `EMAIL_SMTP_PORT`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
