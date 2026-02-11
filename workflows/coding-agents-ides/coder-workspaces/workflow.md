# coder-workspaces

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/developmentcats/coder-workspaces/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/developmentcats/coder-workspaces/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Manage Coder workspaces and AI coding agent tasks via CLI. List, create, start, stop, and delete workspaces. SSH into workspaces to run commands. Create and monitor AI coding tasks with Claude Code, Aider, or other agents.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Coder workspaces and AI coding agent tasks via CLI. List, create, start, stop, and delete workspaces. SSH into workspaces to run commands. Create and monitor AI coding tasks with Claude Code, Aider, or other agents.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run coder-workspaces`)
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
You are executing the coder-workspaces workflow. Use the following context:

Description: Manage Coder workspaces and AI coding agent tasks via CLI. List, create, start, stop, and delete workspaces. SSH into workspaces to run commands. Create and monitor AI coding tasks with Claude Code, Aider, or other agents.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: coder-workspaces
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Coder Workspaces

Manage Coder workspaces and AI coding agent tasks via the coder CLI.

> Note: Commands execute within isolated, governed Coder workspaces — not the host system.

## Setup

Before using coder CLI, configure authentication:

1. Install the CLI from [Coder CLI docs](https://coder.com/docs/install/cli)

2. Set environment variables:
   ```bash
   export CODER_URL=https://your-coder-instance.com
   export CODER_SESSION_TOKEN=<your-token>  # Get from /cli-auth
   ```

3. Test connection:
   ```bash
   coder whoami
   ```

## Workspace Commands

```bash
coder list                              # List workspaces
coder list --all                        # Include stopped
coder list -o json                      # JSON output

coder start <workspace>
coder stop <workspace>
coder restart <workspace> -y
coder delete <workspace> -y

coder ssh <workspace>                   # Interactive shell
coder ssh <workspace> -- <command>      # Run command in workspace

coder logs <workspace>
coder logs <workspace> -f               # Follow logs
```

## AI Coding Tasks

Coder Tasks runs AI agents (Claude Code, Aider, etc.) in isolated workspaces.

### Creating Tasks

```bash
coder tasks create --template <template> --preset "<preset>" "prompt"
```

- **Template**: Required. List with `coder templates list`
- **Preset**: May be required. Try without first. If creation fails with "Required parameter not provided", get presets with `coder templates presets list <template> -o json` and use the default. If no default, ask user which preset.

### Managing Tasks

```bash
coder tasks list                        # List all tasks
coder tasks logs <task-name>            # View output
coder tasks connect <task-name>         # Interactive session
coder tasks delete <task-name> -y       # Delete task
```

### Task States

- **Initializing**: Workspace provisioning (timing varies by template)
- **Working**: Setup script running
- **Active**: Agent processing prompt
- **Idle**: Agent waiting for input

## Troubleshooting

- **CLI not found**: See [Coder CLI docs](https://coder.com/docs/install/cli)
- **Auth failed**: Verify CODER_URL and CODER_SESSION_TOKEN are set, then run `coder login`
- **Version mismatch**: Reinstall CLI from your Coder instance

## More Info

- [Coder Docs](https://coder.com/docs)
- [Coder CLI](https://coder.com/docs/install/cli)
- [Coder Tasks](https://coder.com/docs/ai-coder)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
