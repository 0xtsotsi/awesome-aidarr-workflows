# ping-beads

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xejrax/ping-beads/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xejrax/ping-beads/SKILL.md)
> Category: Marketing & Sales

---

## Description

Verify the bead daemon is alive and responsive

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Verify the bead daemon is alive and responsive

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run ping-beads`)
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
You are executing the ping-beads workflow. Use the following context:

Description: Verify the bead daemon is alive and responsive

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ping-beads
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Ping Beads

Verify the bead daemon is alive and responsive. Checks the `bd.sock` socket to confirm the bead daemon (`bd`) is running and accepting connections.

## Commands

```bash
# Check if the bead daemon is alive (checks bd.sock)
ping-beads

# Show detailed bead daemon status
ping-beads status
```

## Install

No installation needed. `bd` is expected to be in PATH as part of the beads system.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
