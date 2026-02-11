# voicenotes

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/shawnhansen/voicenotes/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/shawnhansen/voicenotes/SKILL.md)
> Category: CLI Utilities

---

## Description

Sync and access voice notes from Voicenotes.com. Use when the user wants to retrieve their voice recordings, transcripts, and AI summaries from Voicenotes. Supports fetching notes, syncing to markdown, and searching transcripts.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Sync and access voice notes from Voicenotes.com. Use when the user wants to retrieve their voice recordings, transcripts, and AI summaries from Voicenotes. Supports fetching notes, syncing to markdown, and searching transcripts.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run voicenotes`)
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
You are executing the voicenotes workflow. Use the following context:

Description: Sync and access voice notes from Voicenotes.com. Use when the user wants to retrieve their voice recordings, transcripts, and AI summaries from Voicenotes. Supports fetching notes, syncing to markdown, and searching transcripts.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: voicenotes
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Voicenotes Integration

Sync voice notes from [voicenotes.com](https://voicenotes.com) into the workspace.

## Setup

1. Get access token from: https://voicenotes.com/app?obsidian=true#settings
2. Set environment variable: `export VOICENOTES_TOKEN="your-token-here"`

## Quick Start

```bash
# Verify connection
./scripts/get-user.sh | jq .

# Fetch recent notes (JSON)
./scripts/fetch-notes.sh | jq '.data[:3]'

# Sync all notes to markdown files
./scripts/sync-to-markdown.sh --output-dir ./voicenotes
```

## Scripts

### fetch-notes.sh
Fetch voice notes as JSON.
```bash
./scripts/fetch-notes.sh                    # All notes
./scripts/fetch-notes.sh --limit 10         # Last 10 notes
./scripts/fetch-notes.sh --since 2024-01-01 # Notes since date
```

### get-user.sh
Verify token and get user info.
```bash
./scripts/get-user.sh | jq '{name, email}'
```

### sync-to-markdown.sh
Sync notes to markdown files with frontmatter.
```bash
./scripts/sync-to-markdown.sh --output-dir ./voicenotes
```

Output format:
```markdown
---
voicenotes_id: abc123
created: 2024-01-15T10:30:00Z
tags: [idea, project]
---

# Note Title

## Transcript
The transcribed content...

## Summary
AI-generated summary...
```

## API Reference

Base URL: `https://api.voicenotes.com/api/integrations/obsidian-sync`

Headers required:
- `Authorization: Bearer {token}`
- `X-API-KEY: {token}`

Endpoints:
- `GET /user/info` - User details
- `GET /recordings` - List voice notes (paginated)
- `GET /recordings/{id}/signed-url` - Audio download URL

## Data Structure

Each voice note contains:
- `recording_id` - Unique identifier
- `title` - Note title
- `transcript` - Full transcript text
- `creations[]` - AI summaries, action items, etc.
- `tags[]` - User tags
- `created_at` / `updated_at` - Timestamps
- `duration` - Recording length in seconds

## Tips

- Notes are paginated; check `links.next` for more pages
- Use `--since` to fetch only new notes since last sync
- AI creations include summaries, todos, and custom prompts
- Rate limited to ~60 requests/minute

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
