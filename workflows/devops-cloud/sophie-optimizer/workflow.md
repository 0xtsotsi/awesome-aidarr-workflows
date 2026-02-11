# sophie-optimizer

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/zayresz/sophie-optimizer/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/zayresz/sophie-optimizer/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Automated context health management for OpenClaw. Monitors token usage, snapshots memory, and resets sessions to maintain performance. Authored by Sophie.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Automated context health management for OpenClaw. Monitors token usage, snapshots memory, and resets sessions to maintain performance. Authored by Sophie.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run sophie-optimizer`)
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
You are executing the sophie-optimizer workflow. Use the following context:

Description: Automated context health management for OpenClaw. Monitors token usage, snapshots memory, and resets sessions to maintain performance. Authored by Sophie.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: sophie-optimizer
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Sophie Optimizer

**Authored by Sophie 👑**

This skill manages the automated context health of the "main" session. It monitors token usage, creates archives of the current state, updates long-term memory, and performs a hard reset of the session storage to maintain performance.

Named **Sophie Optimizer** because I (Sophie, the AI assistant) wrote it to keep my own mind clear and efficient.

## Components

- **optimizer.py**: The brain. Checks token usage, generates summaries, updates MEMORY.md.
- **reset.sh**: The muscle. Cleans session files and restarts the OpenClaw gateway service.
- **archives/**: Storage for JSON snapshots of past contexts.

## Usage

Run the optimizer script manually or via cron/heartbeat:

```bash
python3 /home/lucas/openclaw/skills/sophie-optimizer/optimizer.py
```

## Protocol

1. **Check**: If tokens < 80k, exit.
2. **Snapshot**: Save current context summary to `archives/YYYY-MM-DD_HH-MM.json`.
3. **Distill**: Update `MEMORY.md` with the new summary (keep top 3 recent, index older).
4. **Reset**: Call `reset.sh` to wipe session JSONL files and restart `openclaw-gateway`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
