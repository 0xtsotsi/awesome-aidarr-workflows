# n8n-monitor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/smitti7971/n8n-monitor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/smitti7971/n8n-monitor/SKILL.md)
> Category: DevOps & Cloud

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
**Trigger:** User-invocable (via `aidarr run n8n-monitor`)
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
You are executing the n8n-monitor workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: n8n-monitor
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Skill: n8n-monitor

Monitoramento operacional do N8N via Docker.

## Capabilities
- Verificar status dos containers N8N
- Ler logs recentes
- Checar saúde do container
- Analisar uso de CPU e memória

## Commands
- docker ps | grep n8n
- docker logs --tail 50 n8n
- docker inspect --format='{{.State.Health.Status}}' n8n
- docker stats --no-stream n8n

## Output
Respostas em Markdown, com tabelas simples e status claro.

## Status
active

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
