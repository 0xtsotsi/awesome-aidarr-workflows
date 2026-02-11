# task-status

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mightyprime1/task-status/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mightyprime1/task-status/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Send short status descriptions in chat for long-running tasks. Use when you need to provide periodic updates during multi-step operations, confirm task completion, or notify of failures. Includes automated periodic monitoring that sends updates every 5 seconds, status message templates, and a helper function for consistent status reporting.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Send short status descriptions in chat for long-running tasks. Use when you need to provide periodic updates during multi-step operations, confirm task completion, or notify of failures. Includes automated periodic monitoring that sends updates every 5 seconds, status message templates, and a helper function for consistent status reporting.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run task-status`)
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
You are executing the task-status workflow. Use the following context:

Description: Send short status descriptions in chat for long-running tasks. Use when you need to provide periodic updates during multi-step operations, confirm task completion, or notify of failures. Includes automated periodic monitoring that sends updates every 5 seconds, status message templates, and a helper function for consistent status reporting.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: task-status
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Task Status Skill

## Quick Start

### Manual Status Updates
```bash
python scripts/send_status.py "Starting data fetch..." "progress" "step1"
python scripts/send_status.py "Processing complete" "success" "final"
python scripts/send_status.py "Error: Missing API key" "error" "auth"
```

### Automatic Periodic Monitoring (Every 5 seconds)
```bash
# Start monitoring a long-running task
python scripts/monitor_task.py start "My Long Task" "processing"

# Monitor will send "Still working..." updates every 5 seconds
# When task completes, report final status
python scripts/monitor_task.py stop "My Long Task" "success" "Completed successfully!"
```

## Status Types

- **progress**: Ongoing work (shows 🔄 or ->)
- **success**: Task complete (shows ✅ or OK)
- **error**: Failed task (shows ❌ or !)
- **warning**: Issue but continuing (shows ⚠️ or ?)

## Periodic Monitoring

The `monitor_task.py` script provides automatic updates:

### Starting Monitor
```bash
python scripts/monitor_task.py start "<task_name>" "<status_type>" [--interval <seconds>]
```

- Automatically sends "Still working..." updates every 5 seconds
- Runs in background until stopped
- Can be customized with different intervals

### Stopping Monitor
```bash
python scripts/monitor_task.py stop "<task_name>" "<final_status>" "<final_message>"
```

### Example: Long File Processing
```bash
# Start monitoring
python scripts/monitor_task.py start "video_processing" "progress"

# ... long processing happens here ...

# Stop with final status
python scripts/monitor_task.py stop "video_processing" "success" "Processing complete!"
```

## Manual Updates (Quick Status)

For single status updates without monitoring:

```bash
python scripts/send_status.py "Still fetching data..." "progress" "fetch"
python scripts/send_status.py "Processing records: 250/1000" "progress" "process"
python scripts/send_status.py "Complete! 3 files ready" "success" "final"
python scripts/send_status.py "Error: Connection timeout" "error" "api"
```

## When to Use Each Method

### Use Manual Updates When:
- Task is short (under 30 seconds)
- You want control over when updates are sent
- Task has discrete, meaningful milestones

### Use Periodic Monitoring When:
- Task is long-running (over 1 minute)
- You want consistent "heartbeat" updates every 5 seconds
- Task has long periods of quiet work
- You want to reassure user that work is ongoing

## Message Guidelines

Keep status messages under 140 characters. Examples:

- **Progress**: "Still fetching data..." or "Processing records: 250/1000"
- **Success**: "Complete! 3 files ready" or "Task finished successfully"
- **Error**: "Error: Connection timeout" or "Failed: Missing API key"
- **Warning**: "Continuing despite timeout" or "Partial success: 5/10 files"

## Advanced Usage

### With Additional Details
```bash
python scripts/send_status.py "Uploading..." "progress" "upload" --details "File: report.pdf (2.4MB)"
```

### Different Intervals
```bash
python scripts/monitor_task.py start "data_sync" "progress" --interval 10
```

### Importing for Python Scripts
```python
from send_status import send_status

def long_task():
    send_status("Starting...", "progress", "step1")
    # ... work
    send_status("Step complete", "success", "step1")
```

## Automation with Clawdbot Cron

For scheduled tasks, use Clawdbot's cron feature:

```python
# In a script or session
from cron import add

# Every 5 seconds, check status
job = {
    "text": "Check status update",
    "interval": "5s",
    "enabled": True
}
add(job)
```

This allows status updates even when you're not actively watching.

## Installation

To use this skill, copy the `task-status` folder into your Clawdbot skills directory:

```
C:\Users\Luffy\AppData\Roaming\npm\node_modules\clawdbot\skills\task-status
```

Or add it to your workspace and reference it from `AGENTS.md` or `TOOLS.md`.

Once installed, the skill will be available for any task where you need periodic status updates.
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
