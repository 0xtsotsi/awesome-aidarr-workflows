# workspace

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/massiveadam/workspace/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/massiveadam/workspace/SKILL.md)
> Category: Clawdbot Tools

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run workspace`)
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
You are executing the workspace workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: workspace
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Gork Legacy Skill

Replication of the "Gork" assistant functionality within OpenClaw.

## Features
- **Task Management**: AI-powered task extraction from notes and Slack.
- **Daily Note Automation**: Automated rollover of incomplete tasks and template generation.
- **Sync Integrations**:
    - **Slack**: Sync DMs and mentions into the vault.
    - **Strava**: Sync fitness activities and HR zone metrics.
    - **Harvest**: Start/stop timers and summarize billable hours.

## Configuration (TOOLS.md)

Add these to your `TOOLS.md`:

```markdown
### Gork Skill
- SLACK_USER_TOKEN: xoxp-...
- STRAVA_CLIENT_ID: ...
- STRAVA_CLIENT_SECRET: ...
- STRAVA_REFRESH_TOKEN: ...
- HARVEST_ACCESS_TOKEN: ...
- HARVEST_ACCOUNT_ID: ...
- OBSIDIAN_VAULT_PATH: /home/adam/.openclaw/workspace/vault
```

## Database Schema (SQL)

The skill uses a local SQLite database `gork.db` with the following tables:
- `tasks`: Centralized task store.
- `strava_activities`: Fitness history.
- `note_processing_log`: Audit trail for vault changes.

## Logic Implementation

### Task Rollover
Instead of modifying files directly via shell scripts, the OpenClaw agent uses the `read` and `write` tools to:
1. Identify the previous day's daily note.
2. Extract lines matching `- [ ]`.
3. Prepend them to the "Overdue" section of today's note.

### Sync Logic
- **Slack**: Periodic poll via `web_fetch` or a dedicated Python script (as seen in legacy).
- **Strava/Harvest**: REST API calls to fetch data and update the local DB.

## File Conflict Resolution
To avoid Obsidian sync conflicts:
1. **Atomic Writes**: Always read the current file content before writing.
2. **Buffer Scratch**: Users write to a "Scratch" section; OpenClaw clears it only after successful processing and commit.
3. **External DB**: Tasks are mirrored in SQLite to ensure no loss if a file sync fails.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
