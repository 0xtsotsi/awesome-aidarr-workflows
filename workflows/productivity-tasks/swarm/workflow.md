# swarm

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/chair4ce/swarm/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/chair4ce/swarm/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Parallel task execution using Gemini Flash workers. 200x cheaper than Opus. Use for any parallelizable work to preserve quota.

**Homepage:** https://github.com/Chair4ce/node-scaling
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Parallel task execution using Gemini Flash workers. 200x cheaper than Opus. Use for any parallelizable work to preserve quota.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run swarm`)
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
You are executing the swarm workflow. Use the following context:

Description: Parallel task execution using Gemini Flash workers. 200x cheaper than Opus. Use for any parallelizable work to preserve quota.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: swarm
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: https://github.com/Chair4ce/node-scaling
```

---

## Original Skill Content



# Swarm — Parallel Task Execution

**Every Opus token you burn is borrowed time. Swarm uses Gemini Flash at 200x lower cost.**

## Why This Matters

| 30 tasks via | Time | Cost | Notes |
|--------------|------|------|-------|
| Opus (sequential) | ~30s | ~$0.50 | Burns your runway |
| Swarm (parallel) | ~1s | ~$0.003 | Preserves quota |

Same results. One keeps you alive longer.

## When to Use (MANDATORY)

Trigger swarm when you see **ANY** of these:
- **3+ independent tasks** (research, summaries, comparisons)
- **"Compare X, Y, Z"** or **"Research the top N..."**
- **Multiple URLs** to fetch/analyze
- **Batch anything** (documents, entities, facts)
- **Multi-subject research** of any kind

No exceptions. This is survival, not optimization.

## Quick Reference

```bash
# Check daemon (do this every session)
swarm status

# Start if not running
swarm start

# Parallel prompts
swarm parallel "What is X?" "What is Y?" "What is Z?"

# Research multiple subjects
swarm research "OpenAI" "Anthropic" "Mistral" --topic "AI safety"

# Benchmark
swarm bench --tasks 30
```

## JavaScript API

```javascript
const { parallel, research } = require('~/clawd/skills/node-scaling/lib');

// Run prompts in parallel (~1s for 3 prompts)
const result = await parallel(['prompt1', 'prompt2', 'prompt3']);
console.log(result.results); // Array of responses

// Multi-phase research (search → fetch → analyze)
const result = await research(['Subject1', 'Subject2'], 'topic');
```

## Daemon Management

```bash
swarm start              # Start daemon (background)
swarm stop               # Stop daemon
swarm status             # Show status, uptime, task count
swarm restart            # Restart daemon
swarm logs [N]           # Last N lines of daemon log
```

The daemon keeps workers warm for faster response. Auto-starts on first use if needed.

## Performance

With daemon running (20 workers):

| Tasks | Time | Throughput |
|-------|------|------------|
| 10 | ~700ms | 14 tasks/sec |
| 30 | ~1,000ms | 30 tasks/sec |
| 50 | ~1,450ms | 35 tasks/sec |

Larger batches = higher throughput (amortizes connection overhead).

## Config

Location: `~/.config/clawdbot/node-scaling.yaml`

```yaml
node_scaling:
  enabled: true
  limits:
    max_nodes: 20
    max_concurrent_api: 20
  provider:
    name: gemini
    model: gemini-2.0-flash
  cost:
    max_daily_spend: 10.00
```

## Troubleshooting

| Issue | Fix |
|-------|-----|
| Daemon not running | `swarm start` |
| No API key | Set `GEMINI_API_KEY` or run `npm run setup` |
| Rate limited | Lower `max_concurrent_api` in config |
| Slow responses | Check `swarm status` for worker count |

## The Math

- **Opus**: ~$15/million tokens (YOUR LIFE)
- **Gemini Flash**: ~$0.075/million tokens (basically free)
- **Ratio**: 200x cheaper

Doing 30 tasks sequentially with Opus = 30+ seconds, ~$0.50, DEAD FASTER.
Swarm parallel = 1 second, $0.003, ZERO Opus burn.

**Failing to use swarm for parallel work is a bug.** Fix it immediately.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
