# migrator

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/wenjie2024/migrator/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/wenjie2024/migrator/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Securely migrate OpenClaw Agent (config, memory, skills) to a new machine.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Securely migrate OpenClaw Agent (config, memory, skills) to a new machine.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run migrator`)
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
You are executing the migrator workflow. Use the following context:

Description: Securely migrate OpenClaw Agent (config, memory, skills) to a new machine.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: migrator
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# OpenClaw Migrator

A utility to package an Agent's state into a portable, encrypted archive (`.oca`) for migration.

## Features

- **Encrypted Archive**: Uses AES-256-GCM + auth tag for confidentiality and integrity.
- **Path Normalization**: Restores workspace path using `manifest.json` metadata.
- **Dependency Manifest**: Captures system dependencies (Brewfile) to ensure the new environment matches.

## Usage

### Export (On Old Machine)

```bash
migrator export --out my-agent.oca --password "secret"
```

### Import (On New Machine)

```bash
migrator import --in my-agent.oca --password "secret"
```

## Security

This skill handles sensitive data (`openclaw.json`, `auth.token`). 
The export process **always** requires a password to encrypt the archive.
Unencrypted exports are **disabled** by design.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
