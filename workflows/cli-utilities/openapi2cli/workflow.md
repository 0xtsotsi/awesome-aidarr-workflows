# openapi2cli

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/awlevin/openapi2cli/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/awlevin/openapi2cli/SKILL.md)
> Category: CLI Utilities

---

## Description

Generate CLI tools from OpenAPI specs. Built for AI agents who hate writing curl commands.

**Homepage:** https://github.com/Olafs-World/openapi2cli
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate CLI tools from OpenAPI specs. Built for AI agents who hate writing curl commands.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run openapi2cli`)
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
You are executing the openapi2cli workflow. Use the following context:

Description: Generate CLI tools from OpenAPI specs. Built for AI agents who hate writing curl commands.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openapi2cli
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: https://github.com/Olafs-World/openapi2cli
```

---

## Original Skill Content



# OpenAPI to CLI

Generate command-line tools from OpenAPI/Swagger specs. Perfect for AI agents that need to interact with APIs without writing curl commands.

## Quick Start

```bash
# generate a CLI from any OpenAPI spec
uvx openapi2cli generate https://api.example.com/openapi.json --output my-api

# use the generated CLI
python my-api.py users list
python my-api.py users get --id 123
python my-api.py posts create --title "Hello" --body "World"
```

## Features

- **Auto-generates CLI** from OpenAPI 3.x specs
- **Supports auth**: API keys, Bearer tokens, Basic auth
- **Rich help**: `--help` on any command shows params
- **JSON output**: Structured responses for parsing
- **Dry-run mode**: See the request without sending

## Usage

```bash
# from URL
uvx openapi2cli generate https://api.example.com/openapi.json -o my-cli

# from local file  
uvx openapi2cli generate ./spec.yaml -o my-cli

# with base URL override
uvx openapi2cli generate ./spec.json -o my-cli --base-url https://api.prod.com
```

## Generated CLI

```bash
# set auth via env
export MY_CLI_API_KEY="sk-..."

# or via flag
python my-cli.py --api-key "sk-..." users list

# see available commands
python my-cli.py --help

# see command options
python my-cli.py users create --help
```

## Example: GitHub API

```bash
uvx openapi2cli generate https://raw.githubusercontent.com/github/rest-api-description/main/descriptions/api.github.com/api.github.com.json -o github-cli

python github-cli.py repos list --owner octocat
```

## Why?

AI agents work better with CLIs than raw HTTP:
- Discoverable commands via `--help`
- Tab completion friendly
- No need to construct JSON payloads
- Easy to chain with pipes

## Links

- [PyPI](https://pypi.org/project/openapi2cli/)
- [GitHub](https://github.com/Olafs-World/openapi2cli)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
