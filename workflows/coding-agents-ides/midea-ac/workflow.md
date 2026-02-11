# midea-ac

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/iamanorange/midea-ac/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/iamanorange/midea-ac/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Control Midea ACs. Use this skill when the user wants to control ACs. Supports turning ACs on/off, setting temperature, setting fan speed, switching modes, and more.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Control Midea ACs. Use this skill when the user wants to control ACs. Supports turning ACs on/off, setting temperature, setting fan speed, switching modes, and more.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run midea-ac`)
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
You are executing the midea-ac workflow. Use the following context:

Description: Control Midea ACs. Use this skill when the user wants to control ACs. Supports turning ACs on/off, setting temperature, setting fan speed, switching modes, and more.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: midea-ac
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Midea Smart Home Control

Control Midea ACs via the msmart.

## How to Use

Skill path: `~/.openclaw/skills/midea_ac`

### AC Control Commands

```bash
# Navigate to skill directory
cd ~/.openclaw/skills/midea_ac

# Check status
python scripts/midea_ac.py bedroom status

# Turn on/off
python scripts/midea_ac.py bedroom on
python scripts/midea_ac.py bedroom off
python scripts/midea_ac.py bedroom toggle

# Set operation mode
python scripts/midea_ac.py bedroom --mode cool

# Set target temperature
python scripts/midea_ac.py bedroom --temperature 26

# Set fan speed
python scripts/midea_ac.py bedroom --fan_speed low

# Set aux hear mode
python scripts/midea_ac.py bedroom --aux_mode on

# Set multiple parameters at once
python scripts/midea_ac.py bedroom --mode heat --temperature 28 --fan_speed medium --aux_mode off
```

## Natural Language Understanding

When the user says the following, execute the corresponding command:

| User Says | Command |
|-----------|---------|
| Turn on the <room-name> AC / open AC | `scripts/midea_ac.py <room-name> on` |
| Turn off the <room-name> AC / close <room-name> AC | `scripts/midea_ac.py <room-name> off` |
| Toggle the <room-name> AC | `scripts/midea_ac.py <room-name> toggle` |
| Warmer / more warm | Check status first, then increase temperature by 2 - 10 degrees |
| Cooler / less heat | Check status first, then decrease temperature by 2 - 10 degrees |
| Full speed / maximum | if mode is heat: `scripts/midea_ac.py <room-name> --temperature 30 --fan_speed max`, if mode is cool: `scripts/midea_ac.py <room-name> --temperature 16 --fan_speed max` |
| Minimum speed | `scripts/midea_ac.py <room-name> --fan_speed low` |
| <room-name> AC status / what's the <room-name> status | `scripts/midea_ac.py <room-name> status` |

## Before Executing

1. Navigate to skill directory: `cd ~/.openclaw/skills/midea_ac`
3. Run with uv: `python scripts/midea_ac.py <room-name> <command>`
3. Report the result to the user after execution

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
