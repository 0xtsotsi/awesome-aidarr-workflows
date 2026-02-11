# digital-ocean

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dbhurley/digital-ocean/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dbhurley/digital-ocean/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Manage Digital Ocean droplets, domains, and infrastructure via DO API.

**Homepage:** https://docs.digitalocean.com/reference/api/
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Digital Ocean droplets, domains, and infrastructure via DO API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run digital-ocean`)
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
You are executing the digital-ocean workflow. Use the following context:

Description: Manage Digital Ocean droplets, domains, and infrastructure via DO API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: digital-ocean
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: https://docs.digitalocean.com/reference/api/
```

---

## Original Skill Content



# Digital Ocean Management

Control DO droplets, domains, and infrastructure.

## Setup

Set environment variable:
- `DO_API_TOKEN`: Your Digital Ocean API token (create at cloud.digitalocean.com/account/api/tokens)

## CLI Commands

```bash
# Account info
uv run {baseDir}/scripts/do.py account

# List all droplets
uv run {baseDir}/scripts/do.py droplets

# Get droplet details
uv run {baseDir}/scripts/do.py droplet <droplet_id>

# List domains
uv run {baseDir}/scripts/do.py domains

# List domain records
uv run {baseDir}/scripts/do.py records <domain>

# Droplet actions
uv run {baseDir}/scripts/do.py power-off <droplet_id>
uv run {baseDir}/scripts/do.py power-on <droplet_id>
uv run {baseDir}/scripts/do.py reboot <droplet_id>
```

## Direct API (curl)

### List Droplets
```bash
curl -s -H "Authorization: Bearer $DO_API_TOKEN" \
  "https://api.digitalocean.com/v2/droplets" | jq '.droplets[] | {id, name, status, ip: .networks.v4[0].ip_address}'
```

### Get Account Info
```bash
curl -s -H "Authorization: Bearer $DO_API_TOKEN" \
  "https://api.digitalocean.com/v2/account" | jq '.account'
```

### List Domains
```bash
curl -s -H "Authorization: Bearer $DO_API_TOKEN" \
  "https://api.digitalocean.com/v2/domains" | jq '.domains[].name'
```

### Create Droplet
```bash
curl -s -X POST -H "Authorization: Bearer $DO_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{
    "name": "my-droplet",
    "region": "nyc1",
    "size": "s-1vcpu-1gb",
    "image": "ubuntu-22-04-x64"
  }' \
  "https://api.digitalocean.com/v2/droplets"
```

### Reboot Droplet
```bash
curl -s -X POST -H "Authorization: Bearer $DO_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"type":"reboot"}' \
  "https://api.digitalocean.com/v2/droplets/<DROPLET_ID>/actions"
```

### Add Domain
```bash
curl -s -X POST -H "Authorization: Bearer $DO_API_TOKEN" \
  -H "Content-Type: application/json" \
  -d '{"name": "example.com"}' \
  "https://api.digitalocean.com/v2/domains"
```

## Notes

- Always confirm before destructive actions (power-off, destroy)
- Token requires read/write scope for management actions
- API docs: https://docs.digitalocean.com/reference/api/api-reference/

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
