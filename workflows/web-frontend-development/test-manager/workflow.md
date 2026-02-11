# test-manager

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/savelieve/test-manager/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/savelieve/test-manager/SKILL.md)
> Category: Web & Frontend Development

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
**Trigger:** User-invocable (via `aidarr run test-manager`)
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
You are executing the test-manager workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: test-manager
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# ClickUp Integration

## Credentials
**Note:** Configure your credentials in TOOLS.md or set environment variables:
- `CLICKUP_API_TOKEN` - Your ClickUp API token
- `CLICKUP_WORKSPACE_ID` - Your ClickUp workspace ID

## User Assignment Guide
When assigning tasks, use the correct email based on who should do the work:

| Email | Who | Use When |
|-------|-----|----------|
| `your-email@example.com` | **Human** | Tasks for you to do manually |
| `ai-assistant@example.com` | **AI Assistant** | Tasks for AI to execute |
| Both emails | **Both Human + AI** | Collaborative tasks where AI does research/writing, human reviews/decides |

### Examples
- **AI-only task**: "Research trend detection tools" → Assign to AI email
- **Human-only task**: "Record video for YouTube" → Assign to your email
- **Collaborative**: "Create content strategy" → Assign to both

## Common Actions

### List Tasks in a List
```http
GET https://api.clickup.com/api/v2/list/{list_id}/task
Authorization: {your_api_token}
```

### Get All Tasks in Workspace
```http
GET https://api.clickup.com/api/v2/team/{workspace_id}/task
Authorization: {your_api_token}
```

### Create Task
```http
POST https://api.clickup.com/api/v2/list/{list_id}/task
Authorization: {your_api_token}
Content-Type: application/json

{
  "name": "Task name",
  "description": "Task description",
  "status": "active"
}
```

### Update Task Status
```http
PUT https://api.clickup.com/api/v2/task/{task_id}
Authorization: {your_api_token}
Content-Type: application/json

{
  "status": "done"
}
```

### Get Task Details
```http
GET https://api.clickup.com/api/v2/task/{task_id}
Authorization: {your_api_token}
```

## Headers for All Requests
```
Authorization: {your_api_token}
Content-Type: application/json
```

## Status Values
Common statuses: `active`, `pending`, `review`, `completed`, `done`

## Error Handling
- 401: Check API token
- 404: Verify list_id or task_id exists
- 429: Rate limited - wait before retrying

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
