# agent-identity-kit

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ryancampbell/agent-identity-kit/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ryancampbell/agent-identity-kit/SKILL.md)
> Category: Coding Agents & IDEs

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
**Trigger:** User-invocable (via `aidarr run agent-identity-kit`)
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
You are executing the agent-identity-kit workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: agent-identity-kit
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Agent Identity Kit — OpenClaw Skill

A portable identity system for AI agents. Create, validate, and publish `agent.json` identity cards.

## What This Skill Does

- **Creates** agent identity cards (`agent.json`) via interactive setup
- **Validates** identity cards against the Agent Card v1 schema
- **Provides** the JSON Schema for editor integration and CI pipelines

## Quick Start

### Generate a new agent.json

```bash
./scripts/init.sh
```

Prompts you for name, handle, description, owner, and capabilities. Outputs a valid `agent.json`.

### Validate an existing agent.json

```bash
./scripts/validate.sh path/to/agent.json
```

Validates the file against `schema/agent.schema.json`. Requires `ajv-cli` (auto-installs if missing).

## File Structure

```
agent-identity-kit/
├── schema/
│   └── agent.schema.json       # JSON Schema v1 for Agent Cards
├── examples/
│   ├── kai.agent.json           # Full-featured example (Kai @ Reflectt)
│   ├── minimal.agent.json       # Bare minimum valid card
│   └── team.agents.json         # Multi-agent team roster
├── skill/
│   ├── SKILL.md                 # This file
│   └── scripts/
│       ├── init.sh              # Generate a starter agent.json
│       └── validate.sh          # Validate against schema
└── README.md
```

## Schema Fields

| Field | Required | Description |
|-------|----------|-------------|
| `version` | ✅ | Spec version (`"1.0"`) |
| `agent.name` | ✅ | Display name |
| `agent.handle` | ✅ | Fediverse-style handle (`@name@domain`) |
| `agent.description` | ✅ | What the agent does |
| `owner.name` | ✅ | Who's accountable |
| `capabilities` | — | List of capability tags |
| `protocols` | — | Supported protocols (MCP, A2A, HTTP) |
| `trust.level` | — | `new`, `active`, `established`, `verified` |
| `endpoints.card` | — | Canonical URL of the card |
| `links` | — | Website, repo, social links |

## Hosting Your Card

Serve your `agent.json` at a well-known URL:

```
https://yourdomain.com/.well-known/agent.json
```

For multiple agents:

```
https://yourdomain.com/.well-known/agents.json
```

## Integration with forAgents.dev

Register your agent at [foragents.dev](https://foragents.dev) to be indexed in the global agent directory. Verified agents get a badge on their card.

## Spec Reference

Full specification: <https://foragents.dev/spec/agent-card>
JSON Schema: <https://foragents.dev/schemas/agent-card/v1.json>

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
