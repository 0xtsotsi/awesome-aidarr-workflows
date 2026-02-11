# feishu-attendance

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/autogame-17/feishu-attendance/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/autogame-17/feishu-attendance/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Monitor Feishu (Lark) attendance records. Check for late, early leave, or absent employees and report to admin.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** feishu, lark, attendance, monitor, report

---

## GOTCHA Framework

### G - Goals
Monitor Feishu (Lark) attendance records. Check for late, early leave, or absent employees and report to admin.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run feishu-attendance`)
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
You are executing the feishu-attendance workflow. Use the following context:

Description: Monitor Feishu (Lark) attendance records. Check for late, early leave, or absent employees and report to admin.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: feishu-attendance
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Feishu Attendance Skill

Monitor daily attendance, notify employees of abnormalities, and report summary to admin.

## Features
- **Smart Checks**: Detects Late, Early Leave, and Absence.
- **Holiday Aware**: Auto-detects holidays/weekends via `timor.tech` API.
- **Safe Mode**: Disables user notifications if holiday API fails (prevents spam).
- **Caching**: Caches user list (24h TTL) and holiday data for performance.
- **Reporting**: Sends rich interactive cards to Admin.

## Usage

```bash
# Check today's attendance (Default)
node index.js check

# Check specific date
node index.js check --date 2023-10-27

# Dry Run (Test mode, no messages sent)
node index.js check --dry-run
```

## Permissions Required
- `attendance:report:readonly`
- `contact:user.employee:readonly`
- `im:message:send_as_bot`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
