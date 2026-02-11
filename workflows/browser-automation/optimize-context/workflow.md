# optimize-context

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/blackworm/optimize-context/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/blackworm/optimize-context/SKILL.md)
> Category: Browser & Automation

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
**Trigger:** User-invocable (via `aidarr run optimize-context`)
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
You are executing the optimize-context workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: optimize-context
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Context Optimizer & Task Processing Skills Package

## Overview
This package contains two powerful OpenClaw skills for automated context management:

1. **Context Optimizer** - Automatically optimizes conversation context to prevent "prompt too large" errors
2. **Task Processor** - Handles large tasks by automatically splitting them into smaller subtasks

## Files Included
- `skills/context-optimizer/` - Main skill directory with all implementation files
- `commands/optimize-context.js` - Command handler for context optimization
- `commands/optimize-context.json` - Command configuration for context optimization
- `commands/process-task.js` - Command handler for processing large tasks
- `commands/process-task.json` - Command configuration for task processing
- `systems/context-monitor.js` - Background context monitoring system
- `systems/context-monitor-config.json` - Configuration for context monitoring
- `task_processing_config.json` - Global task processing configuration

## Installation Instructions

1. Extract this package to your OpenClaw workspace:
   ```bash
   cd ~/.openclaw/workspace
   tar -xzf /path/to/context-optimizer-skill.tar.gz
   ```

2. Install dependencies (if any are needed):
   ```bash
   cd ~/.openclaw/workspace/skills/context-optimizer
   npm install
   ```

3. The skills should now be available in your OpenClaw system with:
   - `/optimize-context` command for manual context optimization
   - `/process-task` command for handling large tasks with automatic splitting

## Features

### Context Optimizer
- Automatically monitors conversation length
- Triggers optimization when message count exceeds thresholds
- Extracts key points and facts while clearing old context
- Prevents "prompt too large" errors

### Task Processor
- Detects large tasks that exceed token limits
- Automatically splits large tasks into smaller subtasks
- Processes subtasks sequentially while maintaining context
- Integrates with context optimization to prevent overflow

### Automatic Monitoring
- Continuous background monitoring of context length
- Configurable thresholds for automatic optimization
- Seamless integration with normal conversation flow

## Configuration
- Adjust settings in `task_processing_config.json`
- Modify thresholds for message counts and token limits
- Configure timing for automatic optimization triggers

The skills are ready to use immediately after installation!
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
