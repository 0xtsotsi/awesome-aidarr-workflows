# codex-quota

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/odrobnik/codex-quota/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/odrobnik/codex-quota/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Check OpenAI Codex CLI rate limit status (daily/weekly quotas) using local session logs. Portable Python script.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Check OpenAI Codex CLI rate limit status (daily/weekly quotas) using local session logs. Portable Python script.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run codex-quota`)
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
You are executing the codex-quota workflow. Use the following context:

Description: Check OpenAI Codex CLI rate limit status (daily/weekly quotas) using local session logs. Portable Python script.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: codex-quota
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Skill: codex-quota

Check OpenAI Codex CLI rate limit status.

## Quick Reference

```bash
# Run the included Python script
./codex-quota.py

# Or if installed to PATH
codex-quota
```

## Options

```bash
codex-quota              # Show current quota (cached from latest session)
codex-quota --fresh      # Ping Codex first for live data
codex-quota --all        # Update all accounts, save to /tmp/codex-quota-all.json
codex-quota --json       # Output as JSON
codex-quota --help       # Show help
```

## What It Shows

- **Primary Window** (5 hours) — Short-term rate limit
- **Secondary Window** (7 days) — Weekly rate limit
- Reset times in local timezone with countdown
- Source session file and age

## Installation

Copy `codex-quota.py` to your path:
```bash
cp skills/codex-quota/codex-quota.py ~/bin/codex-quota
chmod +x ~/bin/codex-quota
```

## How It Works

Codex CLI logs rate limit info in every session file (`~/.codex/sessions/YYYY/MM/DD/*.jsonl`) as part of `token_count` events. This tool:

1. Finds the most recent session file
2. Extracts the last `rate_limits` object
3. Formats and displays it

## When to Use

- Before starting heavy Codex work (check weekly quota)
- When Codex seems slow (might be rate-limited)
- Monitoring quota across multiple accounts

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
