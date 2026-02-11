# hokipoki

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/budjoskop/hokipoki/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/budjoskop/hokipoki/SKILL.md)
> Category: AI & LLMs

---

## Description

Switch AI models without switching tabs using the HokiPoki CLI. Hop between Claude, Codex, and Gemini when one gets stuck. Use when the user wants to request help from a different AI model, hop to another AI, get a second opinion from another model, switch models, share AI subscriptions with teammates, or manage HokiPoki provider/listener mode. Triggers on: 'use codex/gemini for this', 'hop to another model', 'ask another AI', 'get a second opinion', 'switch models', 'hokipoki', 'listen for requests'.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Switch AI models without switching tabs using the HokiPoki CLI. Hop between Claude, Codex, and Gemini when one gets stuck. Use when the user wants to request help from a different AI model, hop to another AI, get a second opinion from another model, switch models, share AI subscriptions with teammates, or manage HokiPoki provider/listener mode. Triggers on: 'use codex/gemini for this', 'hop to another model', 'ask another AI', 'get a second opinion', 'switch models', 'hokipoki', 'listen for requests'.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run hokipoki`)
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
You are executing the hokipoki workflow. Use the following context:

Description: Switch AI models without switching tabs using the HokiPoki CLI. Hop between Claude, Codex, and Gemini when one gets stuck. Use when the user wants to request help from a different AI model, hop to another AI, get a second opinion from another model, switch models, share AI subscriptions with teammates, or manage HokiPoki provider/listener mode. Triggers on: 'use codex/gemini for this', 'hop to another model', 'ask another AI', 'get a second opinion', 'switch models', 'hokipoki', 'listen for requests'.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: hokipoki
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# HokiPoki Skill

Route tasks to different AI CLIs (Claude, Codex, Gemini) via the HokiPoki P2P network. API keys never leave the provider's machine; only encrypted requests and results are exchanged.

## Prerequisites

HokiPoki CLI must be installed and authenticated:

```bash
npm install -g @next-halo/hokipoki-cli
hokipoki login
```

Verify with `hokipoki whoami`. If not installed, guide the user through setup.

## Requesting Help from Another AI

Send a task to a remote AI model. Always use `--json` for parseable output:

```bash
# Specific files
hokipoki request --tool claude --task "Fix the auth bug" --files src/auth.ts --json

# Entire directory
hokipoki request --tool codex --task "Add error handling" --dir src/services/ --json

# Whole project (respects .gitignore)
hokipoki request --tool gemini --task "Review for security issues" --all --json

# Route to a team workspace
hokipoki request --tool claude --task "Optimize queries" --files src/db.ts --workspace my-team --json

# Skip auto-apply (just save the patch)
hokipoki request --tool codex --task "Refactor module" --dir src/ --no-auto-apply --json
```

Tool selection: if the user doesn't specify a tool, ask which model to use or omit `--tool` to let HokiPoki choose.

### Patch Auto-Apply

Patches auto-apply when the target directory is a git repo with committed files. If auto-apply fails, inform the user and suggest:

```bash
git init && git add . && git commit -m "initial"
```

## Provider Mode (Sharing Your AI)

Register and listen for incoming requests:

```bash
# Register as a provider (one-time)
hokipoki register --as-provider --tools claude codex gemini

# Start listening
hokipoki listen --tools claude codex
```

Tasks execute in isolated Docker containers (read-only filesystem, tmpfs workspace, auto-cleanup). Docker must be running.

## Status & Account

```bash
hokipoki whoami      # Current user info
hokipoki status      # Account, workspaces, history
hokipoki dashboard   # Open web dashboard in browser
```

## When to Suggest Hopping

- User is stuck on a problem after multiple attempts
- User asks for a different approach or fresh perspective
- Task involves a domain where another model excels (e.g., Codex for boilerplate, Gemini for large-context analysis)
- User explicitly asks to try another AI

## Full Command Reference

See [references/commands.md](references/commands.md) for all CLI options, auth token locations, and advanced usage.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
