# qiuqiu-helper

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mmogdeveloper/qiuqiu-helper/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mmogdeveloper/qiuqiu-helper/SKILL.md)
> Category: Browser & Automation

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
**Trigger:** User-invocable (via `aidarr run qiuqiu-helper`)
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
You are executing the qiuqiu-helper workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: qiuqiu-helper
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# SKILL.md - Qiuqiu Helper

This is a multi-purpose helper skill for Jesse, designed to automate common workspace tasks.

## Tools

### workspace_summary
- Description: Generates a brief summary of recent changes and current status of the workspace.
- Usage: Just call it to get a pragmatic overview.

### quick_note
- Description: Appends a quick timestamped note to a specified file in the memory folder.
- Parameters:
  - content: The text to save.
  - file: (Optional) Target filename, defaults to today's date.

### clean_logs
- Description: Deletes log files older than a specified number of days to save space.
- Parameters:
  - days: (Optional) Retention period in days, defaults to 7.
  - path: (Optional) Directory to clean, defaults to current logs directory.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
