# ocft

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/stormixus/ocft/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/stormixus/ocft/SKILL.md)
> Category: Communication

---

## Description

P2P file transfer between AI agents via message channels. Supports chunked transfer, IPFS fallback for large files, and trusted peer management.

**Homepage:** https://github.com/stormixus/ocft
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
P2P file transfer between AI agents via message channels. Supports chunked transfer, IPFS fallback for large files, and trusted peer management.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run ocft`)
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
You are executing the ocft workflow. Use the following context:

Description: P2P file transfer between AI agents via message channels. Supports chunked transfer, IPFS fallback for large files, and trusted peer management.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ocft
category: Communication
version: 1.0.0
user_invocable: True
homepage: https://github.com/stormixus/ocft
```

---

## Original Skill Content



# OCFT - OpenClaw File Transfer Protocol

P2P file transfer between AI agents via message channels.

## When to Use

Use this skill when:
- Transferring files between AI agents over chat channels
- Setting up peer-to-peer file sharing with trusted agents
- Sending files through Telegram, Discord, Slack, or any text-based channel
- Need chunked transfer with integrity verification
- Transferring large files using IPFS fallback

## Installation

```bash
npm install -g ocft
```

## Quick Start

```bash
# Initialize your node (generates unique ID and secret)
ocft init

# View your status
ocft status

# Export your connection info to share with peers
ocft export

# Add a trusted peer
ocft add-peer <nodeId> <secret> --name "Friend"

# Or import from URI
ocft import ocft://eyJub2RlSWQ...
```

## CLI Commands

### Core Commands

| Command | Description |
|---------|-------------|
| `ocft init` | Initialize node with unique ID and secret |
| `ocft status` | Show node status and configuration |
| `ocft show-secret` | Display full secret (careful!) |
| `ocft export` | Export connection info as URI |
| `ocft import <uri>` | Import peer from ocft:// URI |
| `ocft verify <secret>` | Verify if a secret matches yours |

### Peer Management

| Command | Description |
|---------|-------------|
| `ocft add-peer <id> <secret>` | Add a trusted peer |
| `ocft remove-peer <id>` | Remove a trusted peer |
| `ocft list-peers` | List all trusted peers |
| `ocft extend-peer <nodeId> <hours>` | Extend a peer's trust expiry |
| `ocft set-ttl <hours>` | Set default secret TTL (0 = no expiry) |

### Configuration

| Command | Description |
|---------|-------------|
| `ocft set-download <dir>` | Set download directory |
| `ocft set-max-size <size>` | Set max file size (e.g., `100MB`, `1GB`) |

### IPFS Fallback (for large files)

| Command | Description |
|---------|-------------|
| `ocft ipfs-enable` | Enable IPFS fallback for large files |
| `ocft ipfs-disable` | Disable IPFS fallback |
| `ocft set-ipfs-provider <provider>` | Set provider: `pinata`, `filebase`, `kubo` |
| `ocft set-ipfs-key <key>` | Set IPFS API key |
| `ocft set-kubo-url <url>` | Set Kubo node API URL |
| `ocft set-ipfs-threshold <size>` | Size threshold for IPFS (e.g., `50MB`) |
| `ocft set-ipfs-gateway <url>` | Set custom public IPFS gateway |

## Features

- 🔗 **Message-based**: Transfer files through existing chat channels
- 📦 **Chunked transfer**: Split large files into small pieces (48KB chunks)
- ✅ **Integrity verification**: SHA-256 hash for chunks and files
- 🤝 **Request/Accept**: Explicit acceptance or auto-accept policy
- 🔒 **Security**: Trusted peer whitelist with secrets
- ⏰ **Secret TTL**: Set expiry time for trust relationships
- 🔄 **Resume**: Resume interrupted transfers from last chunk
- 🌐 **IPFS Fallback**: Use IPFS for files exceeding chunk threshold

## Protocol

OCFT messages use a `🔗OCFT:` prefix with Base64-encoded JSON, allowing file transfers over any text-based channel.

## Limitations

- Chunk size: 48KB (safe for Base64 in messages)
- Default max file size: 100MB (configurable via `set-max-size`)
- Designed for text-based channels
- IPFS fallback requires provider setup (Pinata, Filebase, or local Kubo)

## Links

- **GitHub**: https://github.com/stormixus/ocft
- **npm**: https://www.npmjs.com/package/ocft

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
