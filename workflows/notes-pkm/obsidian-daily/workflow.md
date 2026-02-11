# obsidian-daily

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/bastos/obsidian-daily/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/bastos/obsidian-daily/SKILL.md)
> Category: Notes & PKM

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
**Trigger:** User-invocable (via `aidarr run obsidian-daily`)
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
You are executing the obsidian-daily workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: obsidian-daily
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Obsidian Daily Notes

Interact with Obsidian Daily Notes: create notes, append entries, read by date, and search content.

## Setup

Check if a default vault is configured:

```bash
obsidian-cli print-default --path-only 2>/dev/null && echo "OK" || echo "NOT_SET"
```

If `NOT_SET`, ask the user:
1. **Vault name** (required)
2. **Daily notes folder** (default: vault root, common: `Daily Notes`, `Journal`, `daily`)
3. **Date format** (default: `YYYY-MM-DD`)

Configure the vault:

```bash
obsidian-cli set-default "VAULT_NAME"
```

**Obsidian Daily Notes plugin defaults:**
- Date format: `YYYY-MM-DD`
- New file location: Vault root
- Template file location: (none)

## Date Handling

Get current date:

```bash
date +%Y-%m-%d
```

Cross-platform relative dates (GNU first, BSD fallback):

| Reference | Command |
|-----------|---------|
| Today | `date +%Y-%m-%d` |
| Yesterday | `date -d yesterday +%Y-%m-%d 2>/dev/null \|\| date -v-1d +%Y-%m-%d` |
| Last Friday | `date -d "last friday" +%Y-%m-%d 2>/dev/null \|\| date -v-friday +%Y-%m-%d` |
| 3 days ago | `date -d "3 days ago" +%Y-%m-%d 2>/dev/null \|\| date -v-3d +%Y-%m-%d` |
| Next Monday | `date -d "next monday" +%Y-%m-%d 2>/dev/null \|\| date -v+monday +%Y-%m-%d` |

## Commands

### Open/Create Today's Note

```bash
obsidian-cli daily
```

Opens today's daily note in Obsidian, creating it from template if it doesn't exist.

### Append Entry

```bash
obsidian-cli daily && obsidian-cli create "$(date +%Y-%m-%d).md" --content "$(printf '\n%s' "ENTRY_TEXT")" --append
```

With custom folder:

```bash
obsidian-cli daily && obsidian-cli create "Daily Notes/$(date +%Y-%m-%d).md" --content "$(printf '\n%s' "ENTRY_TEXT")" --append
```

### Read Note

Today:

```bash
obsidian-cli print "$(date +%Y-%m-%d).md"
```

Specific date:

```bash
obsidian-cli print "2025-01-10.md"
```

Relative date (yesterday):

```bash
obsidian-cli print "$(date -d yesterday +%Y-%m-%d 2>/dev/null || date -v-1d +%Y-%m-%d).md"
```

### Search Content

```bash
obsidian-cli search-content "TERM"
```

### Search Notes

Interactive fuzzy finder:

```bash
obsidian-cli search
```

### Specific Vault

Add `--vault "NAME"` to any command:

```bash
obsidian-cli print "2025-01-10.md" --vault "Work"
```

## Example Output

```markdown
- Went to the doctor
- [ ] Buy groceries
- https://github.com/anthropics/skills
- 15:45 This is a log line
```

## Use Cases

**Journal entry:**
```bash
obsidian-cli daily && obsidian-cli create "$(date +%Y-%m-%d).md" --content "$(printf '\n%s' "- Went to the doctor")" --append
```

**Task:**
```bash
obsidian-cli daily && obsidian-cli create "$(date +%Y-%m-%d).md" --content "$(printf '\n%s' "- [ ] Buy groceries")" --append
```

**Link:**
```bash
obsidian-cli daily && obsidian-cli create "$(date +%Y-%m-%d).md" --content "$(printf '\n%s' "- https://github.com/anthropics/skills")" --append
```

**Timestamped log:**
```bash
obsidian-cli daily && obsidian-cli create "$(date +%Y-%m-%d).md" --content "$(printf '\n%s' "- $(date +%H:%M) This is a log line")" --append
```

**Read last Friday:**
```bash
obsidian-cli print "$(date -d 'last friday' +%Y-%m-%d 2>/dev/null || date -v-friday +%Y-%m-%d).md"
```

**Search for "meeting":**
```bash
obsidian-cli search-content "meeting"
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
