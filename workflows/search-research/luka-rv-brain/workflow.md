# luka-rv-brain

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/lraivisto/luka-rv-brain/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/lraivisto/luka-rv-brain/SKILL.md)
> Category: Search & Research

---

## Description

High-velocity research orchestration engine. Manages persistent state, synthesis, and autonomous verification for agents.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
High-velocity research orchestration engine. Manages persistent state, synthesis, and autonomous verification for agents.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run luka-rv-brain`)
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
You are executing the luka-rv-brain workflow. Use the following context:

Description: High-velocity research orchestration engine. Manages persistent state, synthesis, and autonomous verification for agents.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: luka-rv-brain
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# ResearchVault 🦞

Autonomous state manager for agentic research.

## Core Features

- **The Vault**: Local SQLite persistence for `artifacts`, `findings`, and `links`.
- **Divergent Reasoning**: Create `branches` and `hypotheses` to explore parallel research paths.
- **Synthesis Engine**: Automated link-discovery using local embeddings.
- **Active Verification**: Self-correcting agents via `verification_missions`.
- **MCP Server**: Native support for cross-agent collaboration.
- **Watchdog Mode**: Continuous background monitoring of URLs and queries.

## Workflows

### 1. Project Initialization
```bash
uv run python scripts/vault.py init --id "metal-v1" --name "Suomi Metal" --objective "Rising underground bands"
```

### 2. Multi-Source Ingestion
```bash
uv run python scripts/vault.py scuttle "https://reddit.com/r/metal" --id "metal-v1"
```

### 3. Synthesis & Verification
```bash
# Link related findings
uv run python scripts/vault.py synthesize --id "metal-v1"

# Plan verification for low-confidence data
uv run python scripts/vault.py verify plan --id "metal-v1"
```

### 4. MCP Server
```bash
uv run python scripts/vault.py mcp --transport stdio
```

## Environment

Requires Python 3.13 and `uv`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
