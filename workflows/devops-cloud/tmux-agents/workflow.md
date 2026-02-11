# tmux-agents

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/cuba6112/tmux-agents/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/cuba6112/tmux-agents/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Manage background coding agents in tmux sessions. Spawn Claude Code or other agents, check progress, get results.

**Homepage:** https://clawdhub.com/skills/tmux-agents
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage background coding agents in tmux sessions. Spawn Claude Code or other agents, check progress, get results.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tmux-agents`)
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
You are executing the tmux-agents workflow. Use the following context:

Description: Manage background coding agents in tmux sessions. Spawn Claude Code or other agents, check progress, get results.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tmux-agents
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: https://clawdhub.com/skills/tmux-agents
```

---

## Original Skill Content



# Tmux Agents

Run coding agents in persistent tmux sessions. They work in the background while you do other things.

## Available Agents

### ☁️ Cloud Agents (API credits)

| Agent | Command | Best For |
|-------|---------|----------|
| **claude** | Claude Code | Complex coding, refactoring, full projects |
| **codex** | OpenAI Codex | Quick edits, auto-approve mode |
| **gemini** | Google Gemini | Research, analysis, documentation |

### 🦙 Local Agents (FREE via Ollama)

| Agent | Command | Best For |
|-------|---------|----------|
| **ollama-claude** | Claude Code + Ollama | Long experiments, heavy refactoring |
| **ollama-codex** | Codex + Ollama | Extended coding sessions |

Local agents use your Mac's GPU — no API costs, great for experimentation!

## Quick Commands

### Spawn a new agent session
```bash
./skills/tmux-agents/scripts/spawn.sh <name> <task> [agent]

# Cloud (uses API credits)
./skills/tmux-agents/scripts/spawn.sh fix-bug "Fix login validation" claude
./skills/tmux-agents/scripts/spawn.sh refactor "Refactor the auth module" codex
./skills/tmux-agents/scripts/spawn.sh research "Research caching strategies" gemini

# Local (FREE - uses Ollama)
./skills/tmux-agents/scripts/spawn.sh experiment "Rewrite entire test suite" ollama-claude
./skills/tmux-agents/scripts/spawn.sh big-refactor "Refactor all services" ollama-codex
```

### List running sessions
```bash
tmux list-sessions
# or
./skills/tmux-agents/scripts/status.sh
```

### Check on a session
```bash
./skills/tmux-agents/scripts/check.sh session-name
```

### Attach to watch live
```bash
tmux attach -t session-name
# Detach with: Ctrl+B, then D
```

### Send additional instructions
```bash
tmux send-keys -t session-name "additional instruction here" Enter
```

### Kill a session when done
```bash
tmux kill-session -t session-name
```

## When to Use Local vs Cloud

| Scenario | Recommendation |
|----------|----------------|
| Quick fix, time-sensitive | ☁️ Cloud (faster) |
| Expensive task, budget matters | 🦙 Local |
| Long experiment, might fail | 🦙 Local |
| Production code review | ☁️ Cloud (smarter) |
| Learning/exploring | 🦙 Local |
| Heavy refactoring | 🦙 Local |

## Parallel Agents

Run multiple agents simultaneously:

```bash
# Mix and match cloud + local
./scripts/spawn.sh backend "Implement user API" claude           # Cloud
./scripts/spawn.sh frontend "Build login form" ollama-codex      # Local
./scripts/spawn.sh docs "Write API documentation" gemini         # Cloud
./scripts/spawn.sh tests "Write all unit tests" ollama-claude    # Local
```

Check all at once:
```bash
./skills/tmux-agents/scripts/status.sh
```

## Ollama Setup

Local agents require Ollama with a coding model:

```bash
# Pull recommended model
ollama pull glm-4.7-flash

# Configure tools (one-time)
ollama launch claude --model glm-4.7-flash --config
ollama launch codex --model glm-4.7-flash --config
```

## Tips

- Sessions persist even if Clawdbot restarts
- Use local agents for risky/experimental work
- Use cloud for production-critical tasks
- Check `tmux ls` to see all active work
- Kill sessions when done to free resources

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
