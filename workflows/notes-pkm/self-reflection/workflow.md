# self-reflection

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/hopyky/self-reflection/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/hopyky/self-reflection/SKILL.md)
> Category: Notes & PKM

---

## Description

Continuous self-improvement through structured reflection and memory

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.1.1

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Continuous self-improvement through structured reflection and memory

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run self-reflection`)
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
You are executing the self-reflection workflow. Use the following context:

Description: Continuous self-improvement through structured reflection and memory

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: self-reflection
category: Notes & PKM
version: 1.1.1
user_invocable: True
homepage: 
```

---

## Original Skill Content



# 🪞 Self-Reflection

A skill for continuous self-improvement. The agent tracks mistakes, lessons learned, and improvements over time through regular heartbeat-triggered reflections.

## Quick Start

```bash
# Check if reflection is needed
self-reflection check

# Log a new reflection
self-reflection log "error-handling" "Forgot timeout on API call" "Always add timeout=30"

# Read recent lessons
self-reflection read

# View statistics
self-reflection stats
```

## How It Works

```
Heartbeat (60m) → Agent reads HEARTBEAT.md → Runs self-reflection check
                                                      │
                                            ┌─────────┴─────────┐
                                            ▼                   ▼
                                           OK              ALERT
                                            │                   │
                                       Continue            Reflect
                                                               │
                                                     ┌─────────┴─────────┐
                                                     ▼                   ▼
                                                   read               log
                                              (past lessons)     (new insights)
```

## Commands

| Command | Description |
|---------|-------------|
| `check [--quiet]` | Check if reflection is due (OK or ALERT) |
| `log <tag> <miss> <fix>` | Log a new reflection |
| `read [n]` | Read last n reflections (default: 5) |
| `stats` | Show reflection statistics |
| `reset` | Reset the timer |

## OpenClaw Integration

Enable heartbeat in `~/.openclaw/openclaw.json`:

```json
{
  "agents": {
    "defaults": {
      "heartbeat": {
        "every": "60m",
        "activeHours": { "start": "08:00", "end": "22:00" }
      }
    }
  }
}
```

Add to your workspace `HEARTBEAT.md`:

```markdown
## Self-Reflection Check (required)
Run `self-reflection check` at each heartbeat.
If ALERT: read past lessons, reflect, then log insights.
```

## Configuration

Create `~/.openclaw/self-reflection.json`:

```json
{
  "threshold_minutes": 60,
  "memory_file": "~/workspace/memory/self-review.md",
  "state_file": "~/.openclaw/self-review-state.json",
  "max_entries_context": 5
}
```

## Author

Created by [hopyky](https://github.com/hopyky)

## License

MIT

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
