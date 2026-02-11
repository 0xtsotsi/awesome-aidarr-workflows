# nix-mode

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/chronicuser21/nix-mode/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/chronicuser21/nix-mode/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Handle Clawdbot operations in Nix mode (configuration management, environment detection).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Handle Clawdbot operations in Nix mode (configuration management, environment detection).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run nix-mode`)
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
You are executing the nix-mode workflow. Use the following context:

Description: Handle Clawdbot operations in Nix mode (configuration management, environment detection).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: nix-mode
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Clawdbot Nix Mode Skill

This skill handles Clawdbot operations specifically when running in Nix mode.

## Nix Mode Specific Features

### Environment Detection
- Detect when `CLAWDBOT_NIX_MODE=1` is set
- Identify Nix-managed configuration paths
- Recognize Nix-specific error messages and behaviors

### Configuration Management
- Understand that auto-install flows are disabled in Nix mode
- Guide users to proper Nix package management
- Explain why certain self-modification features are unavailable

### Path Handling
- Recognize Nix store paths
- Understand the difference between config and state directories
- Handle `CLAWDBOT_CONFIG_PATH` and `CLAWDBOT_STATE_DIR` appropriately

### Troubleshooting
- Identify Nix-specific remediation messages
- Guide users to proper dependency management via Nix
- Explain the read-only Nix mode banner behavior

## Usage Guidelines

When operating in Nix mode:
1. Do not attempt to auto-install dependencies
2. Direct users to Nix package management instead
3. Respect the immutable nature of Nix installations
4. Advise on proper configuration practices for Nix environments
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
