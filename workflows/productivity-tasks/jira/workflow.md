# jira

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jdrhyne/jira/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jdrhyne/jira/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Manage Jira issues, boards, sprints, and projects via the jira-cli. Search, create, update, and transition issues directly from the command line.

**Homepage:** https://github.com/ankitpokhrel/jira-cli
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Jira issues, boards, sprints, and projects via the jira-cli. Search, create, update, and transition issues directly from the command line.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run jira`)
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
You are executing the jira workflow. Use the following context:

Description: Manage Jira issues, boards, sprints, and projects via the jira-cli. Search, create, update, and transition issues directly from the command line.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: jira
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: https://github.com/ankitpokhrel/jira-cli
```

---

## Original Skill Content



# jira

Use `jira` to manage Jira issues, sprints, and boards. Requires API token setup.

## Setup (once)

1. Generate an API token: https://id.atlassian.com/manage-profile/security/api-tokens
2. Export it: `export JIRA_API_TOKEN="your-token"` (add to ~/.zshrc for persistence)
3. Initialize: `jira init --server https://your-org.atlassian.net --login you@email.com --installation cloud`

## Common commands

### Issues
- List issues: `jira issue list -p PROJECT`
- View issue: `jira issue view PROJ-123`
- Create issue: `jira issue create -p PROJECT -t "Task" -s "Summary" -b "Description"`
- Edit issue: `jira issue edit PROJ-123 -s "New summary"`
- Assign issue: `jira issue assign PROJ-123 "user@email.com"`
- Transition issue: `jira issue move PROJ-123 "In Progress"`
- Comment: `jira issue comment add PROJ-123 "My comment"`
- Search (JQL): `jira issue list -q "project = MKT AND status = 'To Do'"`

### Sprints
- List sprints: `jira sprint list -p PROJECT`
- View active sprint: `jira sprint list -p PROJECT --state active`
- Sprint issues: `jira sprint list -p PROJECT --state active --plain`

### Boards
- List boards: `jira board list -p PROJECT`

### Epics
- List epics: `jira epic list -p PROJECT`
- View epic: `jira epic view PROJ-100`

### Projects
- List projects: `jira project list`

## Output formats
- `--plain` — Tab-separated, no colors (best for scripting)
- `--columns key,summary,status` — Select columns
- `--no-truncate` — Don't truncate long fields

## Tips
- Set default project in config: `~/.config/.jira/.config.yml`
- Use JQL for complex queries: `-q "assignee = currentUser() AND status != Done"`
- Open in browser: `jira open PROJ-123`

## Notes
- Confirm with user before creating/editing/transitioning issues
- For bulk operations, show what will change before executing

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
