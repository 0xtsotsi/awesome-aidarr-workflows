# npm-proxy

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/weird-aftertaste/npm-proxy/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/weird-aftertaste/npm-proxy/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Manage Nginx Proxy Manager (NPM) hosts, certificates, and access lists. Use when the user wants to add a new domain, point a domain to a server/port, enable SSL, or check the status of proxy hosts.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Nginx Proxy Manager (NPM) hosts, certificates, and access lists. Use when the user wants to add a new domain, point a domain to a server/port, enable SSL, or check the status of proxy hosts.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run npm-proxy`)
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
You are executing the npm-proxy workflow. Use the following context:

Description: Manage Nginx Proxy Manager (NPM) hosts, certificates, and access lists. Use when the user wants to add a new domain, point a domain to a server/port, enable SSL, or check the status of proxy hosts.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: npm-proxy
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# NPM Proxy Skill

Manage Nginx Proxy Manager (NPM) via its REST API.

## Configuration

Set the following environment variables:
- `NPM_URL`: The URL of your NPM instance (e.g., `https://npm.example.com`)
- `NPM_EMAIL`: Your NPM admin email
- `NPM_PASSWORD`: Your NPM admin password

## Usage

```bash
# List all proxy hosts
python scripts/npm_client.py hosts

# Get details for a specific host
python scripts/npm_client.py host <host_id>

# Enable/Disable a host
python scripts/npm_client.py enable <host_id>
python scripts/npm_client.py disable <host_id>

# Delete a host
python scripts/npm_client.py delete <host_id>

# List certificates
python scripts/npm_client.py certs
```

## Workflows

### Adding a new Proxy Host
To add a new host, use `curl` directly (the script is currently minimal).
Example payload for `POST /api/nginx/proxy-hosts`:
```json
{
  "domain_names": ["sub.example.com"],
  "forward_scheme": "http",
  "forward_host": "192.168.1.10",
  "forward_port": 8080,
  "access_list_id": 0,
  "certificate_id": 0,
  "ssl_forced": false,
  "meta": {
    "letsencrypt_email": "",
    "letsencrypt_agree": false,
    "dns_challenge": false
  },
  "advanced_config": "",
  "locations": [],
  "block_exploits": true,
  "caching_enabled": false,
  "allow_websocket_upgrade": true,
  "http2_support": true,
  "hsts_enabled": false,
  "hsts_subdomains": false
}
```

### Enabling SSL (Let's Encrypt)
1. List certs with `certs` to see if one exists.
2. Update the host with `certificate_id` and `ssl_forced: true`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
