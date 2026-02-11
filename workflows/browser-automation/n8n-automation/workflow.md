# n8n-automation

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dilomcfly/n8n-automation/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dilomcfly/n8n-automation/SKILL.md)
> Category: Browser & Automation

---

## Description

Manage n8n workflows from OpenClaw via the n8n REST API. Use when the user asks about n8n workflows, automations, executions, or wants to trigger, list, create, activate, or debug n8n workflows. Supports both self-hosted n8n and n8n Cloud instances.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage n8n workflows from OpenClaw via the n8n REST API. Use when the user asks about n8n workflows, automations, executions, or wants to trigger, list, create, activate, or debug n8n workflows. Supports both self-hosted n8n and n8n Cloud instances.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run n8n-automation`)
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
You are executing the n8n-automation workflow. Use the following context:

Description: Manage n8n workflows from OpenClaw via the n8n REST API. Use when the user asks about n8n workflows, automations, executions, or wants to trigger, list, create, activate, or debug n8n workflows. Supports both self-hosted n8n and n8n Cloud instances.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: n8n-automation
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# n8n Automation

Control n8n workflow automation platform via REST API.

## Setup

Set these environment variables (or store in `.n8n-api-config`):

```bash
export N8N_API_URL="https://your-instance.app.n8n.cloud/api/v1"  # or http://localhost:5678/api/v1
export N8N_API_KEY="your-api-key-here"
```

Generate API key: n8n Settings → n8n API → Create an API key.

## Quick Reference

All calls use header `X-N8N-API-KEY` for auth.

### List Workflows
```bash
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_URL/workflows" | jq '.data[] | {id, name, active}'
```

### Get Workflow Details
```bash
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_URL/workflows/{id}"
```

### Activate/Deactivate Workflow
```bash
# Activate
curl -s -X PATCH -H "X-N8N-API-KEY: $N8N_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"active": true}' "$N8N_API_URL/workflows/{id}"

# Deactivate
curl -s -X PATCH -H "X-N8N-API-KEY: $N8N_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"active": false}' "$N8N_API_URL/workflows/{id}"
```

### Trigger Workflow (via webhook)
```bash
# Production webhook
curl -s -X POST "$N8N_API_URL/../webhook/{webhook-path}" \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'

# Test webhook
curl -s -X POST "$N8N_API_URL/../webhook-test/{webhook-path}" \
  -H "Content-Type: application/json" \
  -d '{"key": "value"}'
```

### List Executions
```bash
# All recent executions
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_URL/executions?limit=10" | jq '.data[] | {id, workflowId, status, startedAt}'

# Failed executions only
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_URL/executions?status=error&limit=5"

# Executions for specific workflow
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_URL/executions?workflowId={id}&limit=10"
```

### Get Execution Details
```bash
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_URL/executions/{id}"
```

### Create Workflow (from JSON)
```bash
curl -s -X POST -H "X-N8N-API-KEY: $N8N_API_KEY" \
  -H "Content-Type: application/json" \
  -d @workflow.json "$N8N_API_URL/workflows"
```

### Delete Workflow
```bash
curl -s -X DELETE -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_URL/workflows/{id}"
```

## Common Patterns

### Health Check (run periodically)
List active workflows, check recent executions for errors, report status:
```bash
# Count active workflows
ACTIVE=$(curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_URL/workflows?active=true" | jq '.data | length')

# Count failed executions (last 24h)
FAILED=$(curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_URL/executions?status=error&limit=100" | jq '[.data[] | select(.startedAt > (now - 86400 | todate))] | length')

echo "Active workflows: $ACTIVE | Failed (24h): $FAILED"
```

### Debug Failed Execution
1. List failed executions → get execution ID
2. Fetch execution details → find the failing node
3. Check node parameters and input data
4. Suggest fix based on error message

### Workflow Summary
Parse workflow JSON to summarize: trigger type, node count, apps connected, schedule.

## API Endpoints Reference

See [references/api-endpoints.md](references/api-endpoints.md) for complete endpoint documentation.

## Tips
- API key has full access on non-enterprise plans
- Rate limits vary by plan (cloud) or are unlimited (self-hosted)
- Webhook URLs are separate from API URLs (no auth header needed)
- Use `?active=true` or `?active=false` to filter workflow listings
- Execution data may be pruned based on n8n retention settings

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
