# crimson-devlog-agent

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/crimsondevil333333/crimson-devlog-agent/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/crimsondevil333333/crimson-devlog-agent/SKILL.md)
> Category: DevOps & Cloud

---

## Description

A standardized journaling skill for OpenClaw agents to track progress, tasks, and project status using dev-log-cli.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
A standardized journaling skill for OpenClaw agents to track progress, tasks, and project status using dev-log-cli.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run crimson-devlog-agent`)
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
You are executing the crimson-devlog-agent workflow. Use the following context:

Description: A standardized journaling skill for OpenClaw agents to track progress, tasks, and project status using dev-log-cli.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: crimson-devlog-agent
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# DevLog Skill 🦞

A standardized journaling skill for OpenClaw agents to track progress, tasks, and project status using `dev-log-cli`.

## Description
This skill enables agents to maintain a professional developer log. It's designed to capture context, project milestones, and task statuses in a structured SQLite database.

## Requirements
- `dev-log-cli` (installed via `pipx`)

## Links
- **GitHub**: [https://github.com/CrimsonDevil333333/dev-log-cli](https://github.com/CrimsonDevil333333/dev-log-cli)
- **PyPI**: [https://pypi.org/project/dev-log-cli/](https://pypi.org/project/dev-log-cli/)
- **ClawHub**: [https://clawhub.com/skills/devlog-skill](https://clawhub.com/skills/devlog-skill) (Pending Publication)

## Usage

### 📝 Adding Entries
Agents should use this to log significant progress or blockers.
```bash
devlog add "Finished implementing the auth module" --project "Project Alpha" --status "completed" --tags "auth,feature"
```

### 📋 Listing Logs
View recent activity for context.
```bash
devlog list --project "Project Alpha" --limit 5
```

### 📊 Viewing Stats
Check project health and activity.
```bash
devlog stats --project "Project Alpha"
```

### 🔍 Searching
Find historical context on specific topics.
```bash
devlog search "infinite loop"
```

### 🛠️ Editing/Viewing
Detailed inspection or correction of entries.
```bash
devlog view <id>
devlog edit <id>
```

## Internal Setup
The skill includes a `setup.sh` to ensure the CLI is available.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
