# process-watch

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dbhurley/process-watch/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dbhurley/process-watch/SKILL.md)
> Category: CLI Utilities

---

## Description

Monitor system processes - CPU, memory, disk I/O, network, open files, ports. Find resource hogs, kill runaway processes, track what's consuming your machine.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Monitor system processes - CPU, memory, disk I/O, network, open files, ports. Find resource hogs, kill runaway processes, track what's consuming your machine.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run process-watch`)
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
You are executing the process-watch workflow. Use the following context:

Description: Monitor system processes - CPU, memory, disk I/O, network, open files, ports. Find resource hogs, kill runaway processes, track what's consuming your machine.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: process-watch
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Process Watch

Comprehensive system process monitoring. Goes beyond basic `top` to show:
- CPU & memory usage
- Disk I/O per process
- Network connections
- Open files & handles
- Port bindings
- Process trees

## Commands

### List processes
```bash
process-watch list [--sort cpu|mem|disk|name] [--limit 20]
```

### Top resource consumers
```bash
process-watch top [--type cpu|mem|disk|net] [--limit 10]
```

### Process details
```bash
process-watch info <pid>
# Shows: CPU, memory, open files, network connections, children, environment
```

### Find by name
```bash
process-watch find <name>
# e.g., process-watch find chrome
```

### Port bindings
```bash
process-watch ports [--port 3000]
# What's listening on which port?
```

### Network connections
```bash
process-watch net [--pid <pid>] [--established]
```

### Kill process
```bash
process-watch kill <pid> [--force]
process-watch kill --name "chrome" [--force]
```

### Watch mode
```bash
process-watch watch [--interval 2] [--alert-cpu 80] [--alert-mem 90]
# Continuous monitoring with threshold alerts
```

### System summary
```bash
process-watch summary
# Quick overview: load, memory, disk, top processes
```

## Examples

```bash
# What's eating my CPU?
process-watch top --type cpu

# What's on port 3000?
process-watch ports --port 3000

# Details on a specific process
process-watch info 1234

# Kill all Chrome processes
process-watch kill --name chrome

# Watch with alerts
process-watch watch --alert-cpu 90 --alert-mem 85
```

## Platform Support

- **macOS**: Full support
- **Linux**: Full support  
- **Windows**: Partial (basic process list, no lsof equivalent)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
