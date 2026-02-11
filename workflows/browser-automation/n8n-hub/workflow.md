# n8n-hub

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/codedao12/n8n-hub/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/codedao12/n8n-hub/SKILL.md)
> Category: Browser & Automation

---

## Description

Centralized n8n hub for designing reliable flows (idempotency, retries, HITL) and operating them via the public REST API. Use for planning, JSON output, and lifecycle actions like list/publish/debug.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Centralized n8n hub for designing reliable flows (idempotency, retries, HITL) and operating them via the public REST API. Use for planning, JSON output, and lifecycle actions like list/publish/debug.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run n8n-hub`)
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
You are executing the n8n-hub workflow. Use the following context:

Description: Centralized n8n hub for designing reliable flows (idempotency, retries, HITL) and operating them via the public REST API. Use for planning, JSON output, and lifecycle actions like list/publish/debug.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: n8n-hub
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# n8n Hub

This skill merges two tracks:
1) **Design**: plan dependable workflows and optionally emit `workflow.json`.
2) **Operate**: handle workflows/executions via the public REST API.

## Availability
- Public API access is disabled on free trial plans.
- An upgraded plan is required to use the API.

## Configuration

Suggested environment variables (or store in `.n8n-api-config`):

```bash
export N8N_API_BASE_URL="https://your-instance.app.n8n.cloud/api/v1"  # or http://localhost:5678/api/v1
export N8N_API_KEY="your-api-key-here"
```

Create an API key at: n8n Settings → n8n API → Create an API key.

## Use this skill when
- You want a workflow built for idempotency, retries, logging, and review queues.
- You need importable `workflow.json` plus a runbook template.
- You want to list, publish, deactivate, or debug workflows/executions via API.

## Do not use when
- You need pure code automation without n8n.
- You want to bypass security controls or conceal audit trails.

## Inputs
**Required**
- Trigger type + schedule/timezone
- Success criteria and destinations (email/Drive/DB)

**Optional**
- Existing workflow JSON
- Sample payloads/records
- Dedup keys

## Outputs
- Default: design spec (nodes, data contracts, failure modes)
- On request: `workflow.json` + `workflow-lab.md` (from `assets/workflow-lab.md`)

## Auth header
All requests must include:

```
X-N8N-API-KEY: $N8N_API_KEY
```

## Quick actions (API)

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
curl -s -X POST "$N8N_API_BASE_URL/../webhook/{webhook-path}" \
  -H "Content-Type: application/json" \
  -d '{"key":"value"}'
```

### Executions: list
```bash
curl -s -H "X-N8N-API-KEY: $N8N_API_KEY" \
  "$N8N_API_BASE_URL/executions?limit=10" \
  | jq '.data[] | {id, workflowId, status, startedAt}'
```

### Executions: retry
```bash
curl -s -X POST -H "X-N8N-API-KEY: $N8N_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"loadWorkflow":true}' \
  "$N8N_API_BASE_URL/executions/{id}/retry"
```

## Design workflow checklist
1. Confirm trigger type and schedule/timezone.
2. Define inputs, outputs, and validation rules.
3. Choose dedup keys to keep runs idempotent.
4. Add observability (run_id, logs, status row).
5. Add retry policy and error branches.
6. Send failures to a review queue.
7. Add guardrails to prevent silent failure.

## Endpoint index
See `assets/endpoints-api.md` for the complete endpoint list.

## Notes and tips
- The API playground is available only on self-hosted n8n and uses real data.
- The n8n API node can call the public API from within workflows.
- Webhook URLs do not require the API key header.
- Execution data can be pruned by retention settings.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
