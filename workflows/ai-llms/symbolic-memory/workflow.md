# symbolic-memory

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/th3hypn0tist/symbolic-memory/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/th3hypn0tist/symbolic-memory/SKILL.md)
> Category: AI & LLMs

---

## Description

Stateless symbolic memory effect for LLM agents using SQL facts + canonical semantics, activated via symbols and JIT meaning (PostgreSQL + Ollama).

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Stateless symbolic memory effect for LLM agents using SQL facts + canonical semantics, activated via symbols and JIT meaning (PostgreSQL + Ollama).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run symbolic-memory`)
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
You are executing the symbolic-memory workflow. Use the following context:

Description: Stateless symbolic memory effect for LLM agents using SQL facts + canonical semantics, activated via symbols and JIT meaning (PostgreSQL + Ollama).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: symbolic-memory
category: AI & LLMs
version: 1.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# symbolic-memory

## Purpose

Provide a stateless symbolic memory workflow:
- Store facts + canonical semantics in PostgreSQL
- Expose references as symbols
- Activate meaning just-in-time (budgeted)
- Send only activated facts to the LLM (Ollama)

Rule:
Store semantics. Compute meaning. Never confuse the two.

NOTE

This skill does not rely on agent-local persistent memory for long-term state.

Durable knowledge is stored in a shared, versioned symbolic memory substrate
(as defined in the JIT Symbolic Memory design pattern).

The skill may operate without symbolic memory, but long-term coherence
and multi-agent consistency are only guaranteed when it is present.

## Design pattern

https://github.com/Th3Hypn0tist/random/blob/main/jit-symbolic-memory-design-pattern

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
