# simple-backup

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/vacinc/simple-backup/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/vacinc/simple-backup/SKILL.md)
> Category: CLI Utilities

---

## Description

Backup agent brain (workspace) and body (state) to local folder and optionally sync to cloud via rclone.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Backup agent brain (workspace) and body (state) to local folder and optionally sync to cloud via rclone.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run simple-backup`)
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
You are executing the simple-backup workflow. Use the following context:

Description: Backup agent brain (workspace) and body (state) to local folder and optionally sync to cloud via rclone.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: simple-backup
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Simple Backup

A robust backup script that:
1.  **Auto-detects** workspace and state directories from OpenClaw config
2.  **Allows overrides** for custom/non-standard setups
3.  **Compresses & encrypts** using GPG (AES256)
4.  **Prunes** old backups (Daily/Hourly retention)
5.  **Syncs** to cloud via `rclone` (optional)

## Setup

1.  **Dependencies:**
    ```bash
    brew install rclone gnupg jq
    ```

2.  **Password:** Set encryption password (choose one):
    - File: `~/.openclaw/credentials/backup.key` (recommended)
    - Env: `export BACKUP_PASSWORD="secret"`
    - Config: Add `"password": "secret"` to skill config

3.  **Cloud (Optional):**
    ```bash
    rclone config
    ```

## Usage

```bash
simple-backup
```

## Auto-Detection

By default, paths are auto-detected from `~/.openclaw/openclaw.json`:
- **Workspace:** `agents.defaults.workspace`
- **State:** `~/.openclaw` (where config lives)
- **Backup root:** `<workspace>/BACKUPS`

## Custom Configuration

For non-standard setups, override any path in `~/.openclaw/openclaw.json`:

```json
{
  "skills": {
    "entries": {
      "simple-backup": {
        "config": {
          "workspaceDir": "/custom/path/workspace",
          "stateDir": "/custom/path/state",
          "skillsDir": "/custom/path/skills",
          "backupRoot": "/custom/path/backups",
          "remoteDest": "gdrive:backups"
        }
      }
    }
  }
}
```

## Configuration Reference

| Config Key | Env Var | Auto-Detected | Description |
|------------|---------|---------------|-------------|
| `workspaceDir` | `BRAIN_DIR` | `agents.defaults.workspace` | Agent workspace |
| `stateDir` | `BODY_DIR` | `~/.openclaw` | OpenClaw state dir |
| `skillsDir` | `SKILLS_DIR` | `~/openclaw/skills` | Skills directory |
| `backupRoot` | `BACKUP_ROOT` | `<workspace>/BACKUPS` | Local backup storage |
| `remoteDest` | `REMOTE_DEST` | (none) | Rclone remote path |
| `maxDays` | `MAX_DAYS` | 7 | Days to keep daily backups |
| `hourlyRetentionHours` | `HOURLY_RETENTION_HOURS` | 24 | Hours to keep hourly |
| `password` | `BACKUP_PASSWORD` | (none) | Encryption password |

**Priority:** Config file → Env var → Auto-detect

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
