# mcp-registry-manager

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/orosha-ai/mcp-registry-manager/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/orosha-ai/mcp-registry-manager/SKILL.md)
> Category: AI & LLMs

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
**Trigger:** User-invocable (via `aidarr run mcp-registry-manager`)
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
You are executing the mcp-registry-manager workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: mcp-registry-manager
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# MCP Registry Manager 🌐

Centralized discovery and quality scoring for the exploding MCP (Model Context Protocol) ecosystem.

## What It Does

The MCP ecosystem is growing fast — `awesome-mcp-servers`, `AllInOneMCP`, GitHub — but no unified discovery or quality checks.

**MCP Registry Manager** provides:
- **Unified discovery** — Aggregate servers from multiple sources
- **Quality scoring** — Test coverage, documentation, maintenance status
- **Semantic search** — "Find servers for file operations" (not just keyword search)
- **Install management** — Install/uninstall with dependency resolution
- **Categorization** — Organize by domain (files, databases, APIs, dev tools)

## Problem It Solves

MCP is becoming the "USB-C of agent tools" but:
- Discovery is fragmented (GitHub repos, lists, registries)
- No quality signals (which servers are production-ready?)
- No semantic search (can't find "what does this do?")
- No unified management

## Usage

```bash
# Discover all MCP servers
python3 scripts/mcp-registry.py --discover

# Search semantically
python3 scripts/mcp-registry.py --search "file system operations"

# Get quality report for a server
python3 scripts/mcp-registry.py --score @modelcontext/official-filesystem

# Install a server
python3 scripts/mcp-registry.py --install @modelcontext/official-filesystem

# List installed servers
python3 scripts/mcp-registry.py --list

# Update all installed servers
python3 scripts/mcp-registry.py --update
```

## Quality Score Formula

```
Quality = (0.4 * TestCoverage) + (0.3 * Documentation) + (0.2 * Maintenance) + (0.1 * Community)

Where:
- TestCoverage = % of code covered by tests
- Documentation = README completeness, API docs, examples
- Maintenance = Recent commits, responsive issues
- Community = Stars, forks, contributors
```

## Data Sources

| Source | Type | Coverage |
|---------|--------|-----------|
| awesome-mcp-servers | Curated list | Manual discovery |
| GitHub Search | Repos with `mcp-server` topic | Fresh discoveries |
| AllInOneMCP | API registry | Centralized metadata |
| Klavis AI | MCP integrations | Production services |

## Categories

- **Files** — Filesystem, storage, S3
- **Databases** — PostgreSQL, MongoDB, Redis, SQLite
- **APIs** — HTTP, GraphQL, REST
- **Dev Tools** — Git, Docker, CI/CD
- **Media** — Image processing, video, audio
- **Communication** — Email, Slack, Discord
- **Utilities** — Time, crypto, encryption

## Architecture

```
┌─────────────────┐
│  Discovery      │  ← awesome-mcp, GitHub, AllInOneMCP
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Registry DB    │  ← SQLite/PostgreSQL with metadata
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Quality Scorer │  ← Test coverage, docs, maintenance
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  Semantic Search│  ← Embeddings + vector search
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  CLI Interface  │  ← Install/uninstall/update
└─────────────────┘
```

## Requirements

- Python 3.9+
- requests (for GitHub API)
- sentence-transformers (for semantic search)
- numpy/pandas (for scoring)

## Installation

```bash
# Clone repo
git clone https://github.com/orosha-ai/mcp-registry-manager

# Install dependencies
pip install requests sentence-transformers numpy pandas

# Run discovery
python3 scripts/mcp-registry.py --discover
```

## Inspiration

- **MCP Server Stack guide** — Essential servers list
- **awesome-mcp-servers** — Community-curated directory
- **AllInOneMCP** — Remote MCP registry
- **Klavis AI** — MCP integration platform

## Local-Only Promise

- Registry metadata is cached locally
- Install operations run locally
- No telemetry or data sent to external services

## Version History

- **v0.1** — MVP: Discovery, quality scoring, semantic search
- Roadmap: GitHub integration, CI tests, auto-updates

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
