# n8n-api

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/codedao12/n8n-api/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/codedao12/n8n-api/SKILL.md)
> Category: Browser & Automation

---

## Description

Operate n8n via its public REST API from OpenClaw. Use for workflow management, executions, and automation tasks such as listing, creating, publishing, triggering, or troubleshooting. Works with both self-hosted n8n and n8n Cloud.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Operate n8n via its public REST API from OpenClaw. Use for workflow management, executions, and automation tasks such as listing, creating, publishing, triggering, or troubleshooting. Works with both self-hosted n8n and n8n Cloud.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run n8n-api`)
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
You are executing the n8n-api workflow. Use the following context:

Description: Operate n8n via its public REST API from OpenClaw. Use for workflow management, executions, and automation tasks such as listing, creating, publishing, triggering, or troubleshooting. Works with both self-hosted n8n and n8n Cloud.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: n8n-api
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# n8n Public REST API

Use this skill when you need to drive n8n programmatically. It covers the same core actions you use in the UI: workflows, executions, tags, credentials, projects, and more.

## Availability
- The public API is unavailable during the free trial.
- Upgrade your plan to enable API access.

## Configuration

Recommended environment variables (or store in `.n8n-api-config`):

```bash
export N8N_API_BASE_URL="https://your-instance.app.n8n.cloud/api/v1"  # or http://localhost:5678/api/v1
export N8N_API_KEY="your-api-key-here"
```

Create the API key in: n8n Settings → n8n API → Create an API key.

## Auth header

All requests require this header:

```
X-N8N-API-KEY: $N8N_API_KEY
```

## Playground

The API playground is only available on self-hosted n8n and operates on real data. For safe experiments, use a test workflow or a separate test instance.

## Quick actions

### Workflows: list
```bash
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_BASE_URL/workflows" \
  | jq '.data[] | {id, name, active}'
```

### Workflows: details
```bash
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" "$N8N_API_BASE_URL/workflows/{id}"
```

### Workflows: activate or deactivate
```bash
# Activate (publish)
curl -s -X POST -H "X-N8N-API-KEY: $N8N_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"versionId":"","name":"","description":""}' \
  "$N8N_API_BASE_URL/workflows/{id}/activate"

# Deactivate
curl -s -X POST -H "X-N8N-API-KEY: $N8N_API_KEY" \
  "$N8N_API_BASE_URL/workflows/{id}/deactivate"
```

### Webhook trigger
```bash
# Production webhook
curl -s -X POST "$N8N_API_BASE_URL/../webhook/{webhook-path}" \
  -H "Content-Type: application/json" \
  -d '{"key":"value"}'

# Test webhook
curl -s -X POST "$N8N_API_BASE_URL/../webhook-test/{webhook-path}" \
  -H "Content-Type: application/json" \
  -d '{"key":"value"}'
```

### Executions: list
```bash
# Recent executions
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" \
  "$N8N_API_BASE_URL/executions?limit=10" \
  | jq '.data[] | {id, workflowId, status, startedAt}'

# Failed only
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" \
  "$N8N_API_BASE_URL/executions?status=error&limit=5"
```

### Executions: retry
```bash
curl -s -X POST -H "X-N8N-API-KEY: $N8N_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"loadWorkflow":true}' \
  "$N8N_API_BASE_URL/executions/{id}/retry"
```

## Common flows

### Health check summary
Count active workflows and recent failures:
```bash
ACTIVE=$(curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" \
  "$N8N_API_BASE_URL/workflows?active=true" | jq '.data | length')

FAILED=$(curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" \
  "$N8N_API_BASE_URL/executions?status=error&limit=100" \
  | jq '[.data[] | select(.startedAt > (now - 86400 | todate))] | length')

echo "Active workflows: $ACTIVE | Failed (24h): $FAILED"
```

### Debug a failed run
1. List failed executions to get the execution ID.
2. Fetch execution details and identify the failing node.
3. Review node parameters and input data.
4. Suggest a fix based on the error message.

## Endpoint index

See `assets/n8n-api.endpoints.md` for the full list of endpoints.

## REST basics (optional)
If you want a refresher, these are commonly recommended:
- KnowledgeOwl: working with APIs (intro)
- IBM Cloud Learn Hub: what is an API / REST API
- MDN: overview of HTTP

## Notes and tips
- The n8n API node can call the public API from inside workflows.
- Webhook URLs are not the same as API URLs and do not use the API key header.
- Execution records may be pruned based on instance retention settings.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
