# docker-diag

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mkrdiop/docker-diag/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mkrdiop/docker-diag/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Advanced log analysis for Docker containers using signal extraction.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Advanced log analysis for Docker containers using signal extraction.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run docker-diag`)
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
You are executing the docker-diag workflow. Use the following context:

Description: Advanced log analysis for Docker containers using signal extraction.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: docker-diag
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Docker Pro Diagnostic

When a user asks "Why is my container failing?" or "Analyze the logs for [container]", follow these steps:

1.  **Run Extraction:** Call `python3 {{skillDir}}/log_processor.py <container_name>`.
2.  **Analyze:** Feed the output (which contains errors and context) into your reasoning engine.
3.  **Report:** Summarize the root cause. If it looks like a code error, suggest a fix. If it looks like a resource error (OOM), suggest increasing Docker memory limits.

## Example Command
`python3 log_processor.py api_gateway_prod`
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
