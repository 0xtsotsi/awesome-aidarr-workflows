# memory-hygiene

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dylanbaker24/memory-hygiene/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dylanbaker24/memory-hygiene/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Audit, clean, and optimize Clawdbot's vector memory (LanceDB). Use when memory is bloated with junk, token usage is high from irrelevant auto-recalls, or setting up memory maintenance automation.

**Homepage:** https://github.com/xdylanbaker/memory-hygiene
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Audit, clean, and optimize Clawdbot's vector memory (LanceDB). Use when memory is bloated with junk, token usage is high from irrelevant auto-recalls, or setting up memory maintenance automation.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run memory-hygiene`)
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
You are executing the memory-hygiene workflow. Use the following context:

Description: Audit, clean, and optimize Clawdbot's vector memory (LanceDB). Use when memory is bloated with junk, token usage is high from irrelevant auto-recalls, or setting up memory maintenance automation.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: memory-hygiene
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: https://github.com/xdylanbaker/memory-hygiene
```

---

## Original Skill Content



# Memory Hygiene

Keep vector memory lean. Prevent token waste from junk memories.

## Quick Commands

**Audit:** Check what's in memory
```
memory_recall query="*" limit=50
```

**Wipe:** Clear all vector memory
```bash
rm -rf ~/.clawdbot/memory/lancedb/
```
Then restart gateway: `clawdbot gateway restart`

**Reseed:** After wipe, store key facts from MEMORY.md
```
memory_store text="<fact>" category="preference|fact|decision" importance=0.9
```

## Config: Disable Auto-Capture

The main source of junk is `autoCapture: true`. Disable it:

```json
{
  "plugins": {
    "entries": {
      "memory-lancedb": {
        "config": {
          "autoCapture": false,
          "autoRecall": true
        }
      }
    }
  }
}
```

Use `gateway action=config.patch` to apply.

## What to Store (Intentionally)

✅ Store:
- User preferences (tools, workflows, communication style)
- Key decisions (project choices, architecture)
- Important facts (accounts, credentials locations, contacts)
- Lessons learned

❌ Never store:
- Heartbeat status ("HEARTBEAT_OK", "No new messages")
- Transient info (current time, temp states)
- Raw message logs (already in files)
- OAuth URLs or tokens

## Monthly Maintenance Cron

Set up a monthly wipe + reseed:

```
cron action=add job={
  "name": "memory-maintenance",
  "schedule": "0 4 1 * *",
  "text": "Monthly memory maintenance: 1) Wipe ~/.clawdbot/memory/lancedb/ 2) Parse MEMORY.md 3) Store key facts to fresh LanceDB 4) Report completion"
}
```

## Storage Guidelines

When using memory_store:
- Keep text concise (<100 words)
- Use appropriate category
- Set importance 0.7-1.0 for valuable info
- One concept per memory entry

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
