# hetzner

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/thesethrose/hetzner/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/thesethrose/hetzner/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Hetzner Cloud server management using the hcloud CLI. Manage servers, networks, volumes, firewalls, floating IPs, and SSH keys.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Hetzner Cloud server management using the hcloud CLI. Manage servers, networks, volumes, firewalls, floating IPs, and SSH keys.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run hetzner`)
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
You are executing the hetzner workflow. Use the following context:

Description: Hetzner Cloud server management using the hcloud CLI. Manage servers, networks, volumes, firewalls, floating IPs, and SSH keys.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: hetzner
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Hetzner Cloud Skill

Manage your Hetzner Cloud infrastructure using the `hcloud` CLI.

## Setup

Set your Hetzner Cloud API token:
```bash
export HCLOUD_TOKEN="your_token_here"
```

Or add it to the skill's `.env` file.

## Usage

Common commands:

### Servers
- `servers list` - List all servers
- `servers get <id>` - Get server details
- `servers create <name> <type> <image> <location>` - Create a server
- `servers delete <id>` - Delete a server
- `servers start <id>` - Start server
- `servers stop <id>` - Stop server
- `servers reboot <id>` - Reboot server
- `servers ssh <id>` - SSH into server

### Networks
- `networks list` - List networks
- `networks get <id>` - Get network details

### Floating IPs
- `floating-ips list` - List floating IPs

### SSH Keys
- `ssh-keys list` - List SSH keys

### Volumes
- `volumes list` - List volumes

### Firewalls
- `firewalls list` - List firewalls

## Example Usage

```
You: List my Hetzner servers
Bot: Runs servers list → Shows all your cloud servers

You: Create a new server for testing
Bot: Runs servers create test-server cx11 debian-11 fsn1

You: What's using the most resources?
Bot: Runs servers list and analyzes resource usage
```

**Note:** Requires `HCLOUD_TOKEN` environment variable.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
