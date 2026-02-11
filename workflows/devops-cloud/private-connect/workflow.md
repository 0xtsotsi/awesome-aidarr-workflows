# private-connect

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dantelex/private-connect/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dantelex/private-connect/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Access private services by name, from anywhere. No VPN or SSH tunnels.

**Homepage:** https://privateconnect.co
**Repository:** https://github.com/treadiehq/private-connect
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Access private services by name, from anywhere. No VPN or SSH tunnels.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run private-connect`)
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
You are executing the private-connect workflow. Use the following context:

Description: Access private services by name, from anywhere. No VPN or SSH tunnels.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: private-connect
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: https://privateconnect.co
```

---

## Original Skill Content



# Private Connect

Access private services by name, from anywhere. No VPN or SSH tunnels needed.

## What it does

Private Connect lets you reach private infrastructure (databases, APIs, GPU clusters) using simple names instead of IPs and ports. Share your dev environment with teammates in seconds.

## Commands

### connect_reach
Connect to a private service by name.

**Examples:**
- "Connect me to the staging database"
- "Reach the prod API"
- "Connect to jupyter-gpu"

### connect_status
Show available services and their connection status.

**Examples:**
- "What services are available?"
- "Show my connected services"
- "Is the staging database online?"

### connect_share
Share your current environment with a teammate.

**Examples:**
- "Share my environment"
- "Create a share link that expires in 7 days"
- "Share my setup with the team for a week"

### connect_join
Join a shared environment from a teammate.

**Examples:**
- "Join share code x7k9m2"
- "Connect to Bob's environment"

### connect_clone
Clone a teammate's entire environment setup.

**Examples:**
- "Clone Alice's environment"
- "Set up my environment like the senior dev"

### connect_list_shares
List active environment shares.

**Examples:**
- "Show my active shares"
- "What environments am I sharing?"

### connect_revoke
Revoke a shared environment.

**Examples:**
- "Revoke share x7k9m2"
- "Stop sharing with the contractor"

## Setup

1. Install Private Connect:
```bash
curl -fsSL https://privateconnect.co/install.sh | bash
```

2. Authenticate:
```bash
connect up
```

3. The skill will use your authenticated session.

## Requirements

- Private Connect CLI installed and authenticated
- `connect` command available in PATH


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
