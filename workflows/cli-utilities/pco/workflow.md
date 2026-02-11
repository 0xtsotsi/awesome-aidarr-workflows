# pco

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/rubyrunsstuff/pco/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/rubyrunsstuff/pco/SKILL.md)
> Category: CLI Utilities

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
**Trigger:** User-invocable (via `aidarr run pco`)
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
You are executing the pco workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: pco
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# PCO CLI - Planning Center Services

CLI for the Planning Center Services API. Used for Shadow's church work (FBC Gulfport).

## Repository

https://github.com/rubysworld/pco-cli

## Location

```
/Users/ruby/Projects/pco-cli/pco.ts
```

## Running

```bash
tsx /Users/ruby/Projects/pco-cli/pco.ts <command>
```

Or create an alias:
```bash
alias pco="tsx /Users/ruby/Projects/pco-cli/pco.ts"
```

## Authentication

Credentials stored in `~/.config/pco-cli/config.json`

```bash
# Check auth status
pco auth status

# Setup (interactive)
pco auth setup

# Logout
pco auth logout
```

## Global Options

All list commands support:
- `--json` - Output as JSON (default)
- `--table` - Output as table
- `--quiet` - Output only IDs
- `--limit <n>` - Limit results (default: 25)
- `--offset <n>` - Offset results
- `--all` - Fetch all pages

## Commands

### Organization
```bash
pco org get                    # Get org info
```

### Service Types
```bash
pco service-types list         # List all service types
pco st list                    # Alias
pco service-types get <id>     # Get specific service type
```

### Plans
```bash
# List plans (service-type required)
pco plans list --service-type <id>
pco plans list --service-type <id> --filter future
pco plans list --service-type <id> --filter past

# Get specific plan
pco plans get <planId> --service-type <id>
pco plans get <planId> --service-type <id> --include items,team_members
```

Filters: `future`, `past`, `after`, `before`, `no_dates`

### Plan Items
```bash
pco items list --service-type <id> --plan <planId>
pco items get <itemId> --service-type <id> --plan <planId>
```

### Scheduled People (Team Members)
```bash
pco scheduled list --service-type <id> --plan <planId>
```

### People
```bash
pco people list
pco people list --search "John Doe"
pco people get <id>
```

### Teams
```bash
pco teams list --service-type <id>
pco teams get <teamId> --service-type <id>
```

### Songs
```bash
pco songs list
pco songs list --search "Amazing Grace"
pco songs get <id>
pco songs arrangements <songId>
```

### Media
```bash
pco media list
pco media get <id>
```

### Folders
```bash
pco folders list
pco folders get <id>
```

### Series
```bash
pco series list
pco series get <id>
```

### Tag Groups
```bash
pco tag-groups list
pco tag-groups tags <groupId>
```

### Email Templates
```bash
pco email-templates list
```

### Attachment Types
```bash
pco attachment-types list
```

### Report Templates
```bash
pco report-templates list
```

### Raw API
```bash
# Direct API access
pco api GET /service_types
pco api POST /endpoint --data '{"key": "value"}'
pco api PATCH /endpoint --file data.json
pco api DELETE /endpoint
```

## Common Workflows

### Get This Sunday's Service Plan
```bash
# 1. Find service type ID
pco st list --table

# 2. Get future plans
pco plans list --service-type <id> --filter future --limit 1

# 3. Get plan details with includes
pco plans get <planId> --service-type <id> --include items,team_members
```

### Who's Scheduled This Week?
```bash
pco scheduled list --service-type <id> --plan <planId> --table
```

### Search for a Song
```bash
pco songs list --search "Great Are You Lord"
```

## Notes

- This is for **PCO Services** only (not People, Giving, etc.)
- API docs: https://developer.planning.center/docs/#/apps/services
- Context: Church work only — don't mix with Buape stuff

---

*Updated: 2026-01-08*

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
