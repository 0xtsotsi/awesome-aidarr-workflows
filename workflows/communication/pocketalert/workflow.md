# pocketalert

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/akellacom/pocketalert/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/akellacom/pocketalert/SKILL.md)
> Category: Communication

---

## Description

The Pocket Alert (pocketalert.app) skill for OpenClaw enables OpenClaw agents and workflows to send push notifications to iOS and Android devices. It is used to deliver alerts and updates from automated tasks, workflows, and background processes.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
The Pocket Alert (pocketalert.app) skill for OpenClaw enables OpenClaw agents and workflows to send push notifications to iOS and Android devices. It is used to deliver alerts and updates from automated tasks, workflows, and background processes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run pocketalert`)
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
You are executing the pocketalert workflow. Use the following context:

Description: The Pocket Alert (pocketalert.app) skill for OpenClaw enables OpenClaw agents and workflows to send push notifications to iOS and Android devices. It is used to deliver alerts and updates from automated tasks, workflows, and background processes.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: pocketalert
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Pocket Alert

This skill enables interaction with the [Pocket Alert](https://pocketalert.app) service through its CLI tool.

## Prerequisites

The `pocketalert` CLI must be installed and authenticated:

```bash
# Install (if not already installed)
# Download from https://info.pocketalert.app/cli.html and extract to /usr/local/bin/

# Authenticate with your API key
pocketalert auth <your-api-key>
```

## Quick Reference

### Send Push Notifications

```bash
# Basic notification
pocketalert send -t "Title" -m "Message"

# Full form
pocketalert messages send --title "Alert" --message "Server is down!"

# To specific application
pocketalert messages send -t "Deploy" -m "Build completed" -a <app-tid>

# To specific device
pocketalert messages send -t "Alert" -m "Check server" -d <device-tid>

# To all devices
pocketalert messages send -t "Alert" -m "System update" -d all
```

### List Resources

```bash
# List last messages
pocketalert messages list
pocketalert messages list --limit 50
pocketalert messages list --device <device-tid>

# List applications
pocketalert apps list

# List devices
pocketalert devices list

# List webhooks
pocketalert webhooks list

# List API keys
pocketalert apikeys list
```

### Manage Applications

```bash
# Create application
pocketalert apps create --name "My App"
pocketalert apps create -n "Production" -c "#FF5733"

# Get application details
pocketalert apps get <tid>

# Delete application
pocketalert apps delete <tid>
```

### Manage Devices

```bash
# List devices
pocketalert devices list

# Get device details
pocketalert devices get <tid>

# Delete device
pocketalert devices delete <tid>
```

### Manage Webhooks

```bash
# Create webhook
pocketalert webhooks create --name "GitHub Webhook" --message "*"
pocketalert webhooks create -n "Deploy Hook" -m "Deployed %repository.name% by %sender.login%"
pocketalert webhooks create -n "CI/CD" -m "*" -a <app-tid> -d all

# List webhooks
pocketalert webhooks list

# Get webhook details
pocketalert webhooks get <tid>

# Delete webhook
pocketalert webhooks delete <tid>
```

## Message Template Variables

When creating webhooks, you can use template variables from the incoming payload:

```bash
pocketalert webhooks create \
  --name "GitHub Push" \
  --message "Push to %repository.name%: %head_commit.message%"
```

## Configuration

View or modify configuration:

```bash
# View config
pocketalert config

# Set API key
pocketalert config set api_key <new-api-key>

# Set custom base URL (for self-hosted)
pocketalert config set base_url https://your-api.example.com
```

Configuration is stored at `~/.pocketalert/config.json`.

## CI/CD Integration Examples

```bash
# GitHub Actions / GitLab CI
pocketalert send -t "Build Complete" -m "Version $VERSION deployed"

# Server monitoring with cron
*/5 * * * * /usr/local/bin/pocketalert send -t "Server Health" -m "$(uptime)"

# Service check script
if ! systemctl is-active --quiet nginx; then
  pocketalert send -t "NGINX Down" -m "NGINX is not running on $(hostname)"
fi
```

## Error Handling

The CLI returns appropriate exit codes:
- `0` - Success
- `1` - Authentication or API error
- `2` - Invalid arguments

Always check command output for error details.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
