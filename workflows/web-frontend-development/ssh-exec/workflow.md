# ssh-exec

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xejrax/ssh-exec/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xejrax/ssh-exec/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Run a single command on a remote Tailscale node via SSH without opening an interactive session.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Run a single command on a remote Tailscale node via SSH without opening an interactive session.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run ssh-exec`)
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
You are executing the ssh-exec workflow. Use the following context:

Description: Run a single command on a remote Tailscale node via SSH without opening an interactive session.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ssh-exec
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# SSH Exec Skill

Run a single command on a remote Tailscale node via SSH without opening an interactive session. Requires SSH access to the target (key in `~/.ssh/` or `SSH_AUTH_SOCK`) and `SSH_TARGET` env var (e.g., `100.107.204.64:8022`).

## Execute a Remote Command

Run a command on the target and return stdout/stderr:

```bash
ssh -p 8022 user@100.107.204.64 "uname -a"
```

## Execute with Custom Port

Use the `SSH_TARGET` env var:

```bash
ssh -p "${SSH_PORT:-22}" "$SSH_HOST" "df -h"
```

## Run a Script Remotely

Pipe a local script to the remote host:

```bash
ssh -p 8022 user@100.107.204.64 'bash -s' < local-script.sh
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
