# telegram-cloud-storage

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/oki3505f/telegram-cloud-storage/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/oki3505f/telegram-cloud-storage/SKILL.md)
> Category: DevOps & Cloud

---

## Description

A high-performance Telegram Cloud Storage solution using Teldrive. Turns Telegram into an unlimited cloud drive with a local API/UI.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
A high-performance Telegram Cloud Storage solution using Teldrive. Turns Telegram into an unlimited cloud drive with a local API/UI.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run telegram-cloud-storage`)
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
You are executing the telegram-cloud-storage workflow. Use the following context:

Description: A high-performance Telegram Cloud Storage solution using Teldrive. Turns Telegram into an unlimited cloud drive with a local API/UI.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: telegram-cloud-storage
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Telegram Cloud Storage (Teldrive Edition)

This skill runs [Teldrive](https://github.com/tgdrive/teldrive), a powerful utility that organizes Telegram files and provides a high-speed API/UI for accessing them.

## Features
- **Unlimited Storage**: Uses Telegram as a backend.
- **High Performance**: Written in Go, optimized for speed.
- **UI & API**: Includes a web interface and REST API.
- **AI-Native Client**: Includes `client.py` for agent-based file operations.

## Credits
This skill is a wrapper for [Teldrive](https://github.com/tgdrive/teldrive) by [divyam234](https://github.com/divyam234). All credit for the core engine goes to the original authors.

## Requirements
1. **PostgreSQL Database**: Version 17+ recommended.
2. **pgroonga Extension**: Required for file search within Postgres.
3. **Telegram API**: App ID and Hash from [my.telegram.org](https://my.telegram.org).

## Installation

### 1. Database Setup
Ensure Postgres is running and the `pgroonga` extension is installed.
```sql
CREATE DATABASE teldrive;
\c teldrive
CREATE EXTENSION IF NOT EXISTS pgroonga;
```

### 2. Configure
Run the setup script to generate `config/config.toml`:
```bash
./scripts/setup.sh
```

### 3. Start Server
```bash
./scripts/manage.sh start
```

## Agent Usage
The skill includes a Python client for programmatic access.

### Environment Variables
- `TELDRIVE_TOKEN`: Your JWT token (get this from the UI or `config/token.txt` after login).
- `TELDRIVE_SESSION_HASH`: Your Telegram session hash (found in the `teldrive.sessions` table).

### Commands
```bash
# List files
python3 scripts/client.py list /

# Upload a file
python3 scripts/client.py upload local_file.txt /remote/path

# Download a file
python3 scripts/client.py download <file_id> local_save_path
```

## Directory Structure
- `bin/`: Teldrive binary.
- `config/`: Configuration templates and generated config.
- `scripts/`: Setup, management, and client scripts.
- `logs/`: Application logs.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
