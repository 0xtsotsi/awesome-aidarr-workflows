# agenticflow-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/seanphan/agenticflow-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/seanphan/agenticflow-skill/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Comprehensive guide for building AI workflows, agents, and workforce systems with AgenticFlow. Use when designing workflows with various node types, configuring single agents, or orchestrating workforce collaboration patterns.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Comprehensive guide for building AI workflows, agents, and workforce systems with AgenticFlow. Use when designing workflows with various node types, configuring single agents, or orchestrating workforce collaboration patterns.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run agenticflow-skill`)
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
You are executing the agenticflow-skill workflow. Use the following context:

Description: Comprehensive guide for building AI workflows, agents, and workforce systems with AgenticFlow. Use when designing workflows with various node types, configuring single agents, or orchestrating workforce collaboration patterns.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: agenticflow-skill
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# AgenticFlow Skills

AgenticFlow is a platform for building AI-powered automation workflows, intelligent agents, and workforce systems.

## Quick Navigation

| Topic | When to Use | Reference |
|-------|-------------|-----------|
| **Workflow** | Building automation flows with nodes | [workflow/overview.md](./reference/workflow/overview.md) |
| **Agent** | Creating single intelligent agents | [reference/agent/overview.md](./reference/agent/overview.md) |
| **Workforce** | Orchestrating multiple agents | [reference/workforce/overview.md](./reference/workforce/overview.md) |

---

## Workflow

Workflows are linear automation pipelines composed of sequential nodes. Each node performs a specific action.

| Guide | Description |
|-------|-------------|
| [overview.md](./reference/workflow/overview.md) | Core concepts, schemas, execution model |
| [how-to-build.md](./reference/workflow/how-to-build.md) | Step-by-step build guide |
| [how-to-run.md](./reference/workflow/how-to-run.md) | Execute workflows and handle results |
| [node-types.md](./reference/workflow/node-types.md) | Node type schemas and discovery |
| [connections.md](./reference/workflow/connections.md) | Connection providers and setup |

### Node Types Overview

| Category | Example Node Types | Purpose |
|----------|-------------------|---------|
| **AI/LLM** | `claude_ask`, `openai_chat`, `gemini` | AI model calls, text generation |
| **Image Generation** | `generate_image`, `dall_e` | Create images from prompts |
| **Data Processing** | `json_parse`, `text_transform` | Transform and manipulate data |
| **Integrations** | `slack_send`, `gmail`, `notion` | Connect to 300+ external services (MCPs) |
| **API Calls** | `http_request`, `webhook` | HTTP requests and webhooks |
| **File Operations** | `file_upload`, `pdf_parse` | Upload, download, process files |

> **Note**: Workflows in AgenticFlow are **linear and sequential** - nodes execute top to bottom with no branching or loops.

---

## Agent

An Agent is an AI entity with specific capabilities, tools, and a defined persona.

**To learn about agent configuration, load:** [reference/agent/overview.md](./reference/agent/overview.md)

---

## Workforce

Workforce systems coordinate multiple agents to solve complex tasks collaboratively.

**To understand orchestration patterns, load:** [reference/workforce/overview.md](./reference/workforce/overview.md)

### Common Patterns

- **Supervisor** - One agent delegates to specialists
- **Swarm** - Agents self-organize dynamically
- **Pipeline** - Sequential agent handoffs
- **Debate** - Agents discuss to reach consensus

---

## Glossary

For terminology and definitions, see [reference/glossary.md](./reference/glossary.md).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
