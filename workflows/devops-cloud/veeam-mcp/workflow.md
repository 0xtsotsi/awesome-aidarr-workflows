# veeam-mcp

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jgm2025/veeam-mcp/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jgm2025/veeam-mcp/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Query Veeam Backup & Replication and Veeam ONE via MCP server running in Docker. Provides intelligent backup monitoring, job analysis, capacity planning, and infrastructure health checks.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Query Veeam Backup & Replication and Veeam ONE via MCP server running in Docker. Provides intelligent backup monitoring, job analysis, capacity planning, and infrastructure health checks.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run veeam-mcp`)
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
You are executing the veeam-mcp workflow. Use the following context:

Description: Query Veeam Backup & Replication and Veeam ONE via MCP server running in Docker. Provides intelligent backup monitoring, job analysis, capacity planning, and infrastructure health checks.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: veeam-mcp
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Veeam Intelligence MCP Skill

Interact with Veeam Backup & Replication (VBR) and Veeam ONE through an MCP (Model Context Protocol) server running in Docker.

## Natural Language Commands

When the user asks things like:
- **"What backup jobs failed last night?"**
- **"Show me backup status for all VMs"**
- **"What's my backup repository capacity?"**
- **"Which VMs haven't been backed up recently?"**
- **"Check Veeam ONE alerts"**
- **"Analyze backup performance trends"**

## What This Does

This skill wraps the Veeam Intelligence MCP server (running in Docker) and provides natural language access to:

**Veeam Backup & Replication (VBR):**
- Backup job status and history
- Repository capacity and health
- VM backup status
- Job configuration details
- Failed job analysis

**Veeam ONE:**
- Infrastructure monitoring
- Performance analysis
- Alert management
- Capacity planning
- Trend analysis

## Prerequisites

- Docker installed and running
- Veeam Backup & Replication and/or Veeam ONE with active licenses (not Community Edition)
- **Veeam Intelligence enabled** on your Veeam servers (required for Advanced Mode)
- Admin credentials for Veeam servers

## Installation

### 1. Obtain Veeam Intelligence MCP Server

The Veeam Intelligence MCP server is currently in **beta**. 

**To obtain access:**
- Contact Veeam directly or your Veeam account representative
- Visit the official Veeam community forums
- Check Veeam's official channels for beta program announcements

Once you have the MCP server package, build the Docker image:

```bash
cd /path/to/veeam-mcp-server
docker build -t veeam-intelligence-mcp-server .
```

### 2. Install This Skill

```bash
clawhub install veeam-mcp
```

## Configuration

### Create Credentials File

Create `~/.veeam-mcp-creds.json`:

```json
{
  "vbr": {
    "url": "https://veeam-server.yourdomain.com:443/",
    "username": ".\\administrator",
    "password": "your_secure_password"
  },
  "vone": {
    "url": "https://veeam-one.yourdomain.com:1239/",
    "username": ".\\administrator",
    "password": "your_secure_password"
  }
}
```

**Important:** Lock down the credentials file:
```bash
chmod 600 ~/.veeam-mcp-creds.json
```

### Username Format

- **Local accounts**: Use `".\\username"` format
- **Domain accounts**: Use `"DOMAIN\\username"` or `"username@domain.com"`
- **Escape backslashes**: Single backslash in JSON: `".\\"` not `".\\\\"`

### Enable Veeam Intelligence

For live data queries (Advanced Mode), enable Veeam Intelligence on your Veeam servers:

**Veeam Backup & Replication:**
1. Open Veeam B&R console
2. Go to **Options** → **Veeam Intelligence Settings**
3. Enable the AI assistant

**Veeam ONE:**
1. Open Veeam ONE console
2. Find **Veeam Intelligence** settings
3. Enable the feature

Without this, queries will only return documentation (Basic Mode).

## Usage

### Natural Language (OpenClaw)

Just ask naturally:
```
"What Veeam backup jobs failed yesterday?"
"Show me backup repository capacity"
"Check Veeam ONE alerts"
"Which VMs haven't been backed up this week?"
```

### Command Line Scripts

```bash
# Query VBR
./scripts/query-veeam.sh vbr "What backup jobs ran in the last 24 hours?"

# Query Veeam ONE
./scripts/query-veeam.sh vone "Show current alerts"

# Test connections
./scripts/test-connection.sh vbr
./scripts/test-connection.sh vone

# List available MCP tools
./scripts/list-tools.sh vbr
```

## How It Works

```
User Question → OpenClaw Skill → Docker MCP Server → Veeam API
                                        ↓
                               Veeam Intelligence
                                        ↓
                                 JSON Response
```

1. **Docker Container**: MCP server runs in isolated container
2. **STDIO Transport**: Communicates via standard input/output
3. **Credential Injection**: Env vars passed securely from credentials file
4. **Natural Language**: Veeam Intelligence processes queries with AI

## Troubleshooting

### Connection Test Fails

```bash
# Check credentials file
cat ~/.veeam-mcp-creds.json | jq .

# Test Docker image
docker run -i --rm veeam-intelligence-mcp-server

# Manual connection test
echo '{"jsonrpc":"2.0","method":"initialize","params":{"protocolVersion":"2024-11-05","capabilities":{},"clientInfo":{"name":"test","version":"1.0.0"}},"id":1}' | \
  docker run -i --rm \
    -e PRODUCT_NAME=vbr \
    -e WEB_URL=https://your-server:443/ \
    -e ADMIN_USERNAME='.\administrator' \
    -e ADMIN_PASSWORD='yourpassword' \
    -e ACCEPT_SELF_SIGNED_CERT=true \
    veeam-intelligence-mcp-server
```

### Basic Mode (Documentation Only)

If responses say "Basic mode is active", enable Veeam Intelligence on your servers.

### Username Format Issues

- Try `.\\username` (local account)
- Try `DOMAIN\\username` (domain account)
- Ensure single backslash in JSON

## Security Notes

- Credentials stored locally in `~/.veeam-mcp-creds.json` (chmod 600)
- Docker container runs with non-root user
- HTTPS connections with self-signed cert acceptance
- No credentials exposed in logs or command history
- MCP server communicates via stdin/stdout only

## References

- Veeam Intelligence MCP Server: Contact Veeam for beta access
- [Model Context Protocol](https://modelcontextprotocol.io/)
- [Veeam Intelligence Documentation](https://helpcenter.veeam.com/)

## License

This skill is provided as-is. Veeam Intelligence MCP server is licensed separately.

---

**Need Help?** Open an issue on GitHub or ask in the OpenClaw Discord.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
