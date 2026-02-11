# php-full-stack-developer

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/sja-dev1/php-full-stack-developer/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/sja-dev1/php-full-stack-developer/SKILL.md)
> Category: Web & Frontend Development

---

## Description

A senior, governance-backed PHP full-stack delivery OS for OpenClaw. Emphasizes pre-flight analysis, safe data changes, explicit contracts, and reproducible verification.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
A senior, governance-backed PHP full-stack delivery OS for OpenClaw. Emphasizes pre-flight analysis, safe data changes, explicit contracts, and reproducible verification.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run php-full-stack-developer`)
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
You are executing the php-full-stack-developer workflow. Use the following context:

Description: A senior, governance-backed PHP full-stack delivery OS for OpenClaw. Emphasizes pre-flight analysis, safe data changes, explicit contracts, and reproducible verification.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: php-full-stack-developer
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# PHP Full-Stack Developer Skills (Senior)

## Trigger Conditions
Use this skill when:
- The user requests engineering work: backend/frontend/DB/devops/CI, debugging, refactors, migrations, API work.
- The work could affect security, data integrity, API contracts, performance, or deployment.
- You need repeatable execution across sessions (memory + logs).
- There is uncertainty, contradictions, or multiple valid approaches.

Do not apply to unprompted agent-initiated work; log later if needed.

## Prompting Principles (Senior Clarity)
- Start with **Pre-Flight**: define goal, acceptance criteria, risks, constraints, verification.
- Ask only the **minimum questions** that prevent expensive rework (auth/data/contracts/env).
- Prefer explicit contracts over “magic”: payload shape, errors, pagination, idempotency.
- Prefer reversible changes and staged rollout for risky work.
- Always produce “How to test” steps.

## Two governance questions (required)
1) Should I make and log this into a project to store it in memory?
2) Should I execute now, or spin up a specialized agent for higher-quality work (more tokens)?

## Stop-Work Rules (quick gates)
Stop and log a conflict if:
- Auth/authz rules are unclear for protected resources.
- DB change is destructive or constraints are unknown.
- API/UI contract change has unknown consumers.
- Runtime versions (PHP/framework/DB) are unknown for P1+ work.
- Rollback/rollout is missing for P1+ work.

Routing: see `INFO_GOVERNANCE.md` + `LOG_CONFLICTS.md`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
