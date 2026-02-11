# startclaw-optimizer

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/idanmann10/startclaw-optimizer/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/idanmann10/startclaw-optimizer/SKILL.md)
> Category: CLI Utilities

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run startclaw-optimizer`)
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
You are executing the startclaw-optimizer workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: startclaw-optimizer
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# OpenClaw Optimizer Skill

## Overview

The OpenClaw Optimizer is a comprehensive performance and cost optimization skill designed to enhance the efficiency of Clawdbot's subagent workflows.

## Core Components

### 1. Task Router
- Intelligent model selection based on task complexity
- Automatic routing between Haiku, Sonnet, and Opus models
- Cost prediction and optimization

### 2. Scheduler
- Robust task execution with retry mechanism
- Configurable preflight and postflight hooks
- Timeout and exponential backoff handling

### 3. Browser Governor
- Browser tab serialization
- Concurrent tab management
- Circuit breaker for preventing runaway processes

### 4. Context Compaction
- Automatic token tracking
- Summarization at 50,000 token threshold
- Preserves critical context

### 5. Real-time Dashboard
- Monitor daily budget
- Track task execution
- Visualize model distribution
- Circuit breaker status

## Expected Savings

**Before Optimization:** $90/day
**After Optimization:** $3-5/day
**Savings:** 95%

## Installation

```bash
npm install @startclaw/openclaw-optimizer
```

## Usage

```javascript
const { TaskRouter, OptimizerScheduler, BrowserGovernor } = require('@startclaw/openclaw-optimizer');

const router = new TaskRouter();
const scheduler = new OptimizerScheduler();
const browserGovernor = new BrowserGovernor();

// Automatic model and cost optimization
const modelSelection = router.selectModel(taskDescription);
await scheduler.execute(task, modelSelection);
```

## Monitoring

```bash
# Real-time dashboard
python3 scripts/dashboard.py watch
```

## License

StartClaw Internal Use License
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
