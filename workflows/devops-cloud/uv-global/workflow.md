# uv-global

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/guoqiao/uv-global/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/guoqiao/uv-global/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Provision and reuse a global uv environment for ad hoc Python scripts.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Provision and reuse a global uv environment for ad hoc Python scripts.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run uv-global`)
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
You are executing the uv-global workflow. Use the following context:

Description: Provision and reuse a global uv environment for ad hoc Python scripts.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: uv-global
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# UV Global

Create and reuse a global `uv` environment at `~/.uv-global` so you can install Python dependencies for quick, ad hoc scripts without polluting the system interpreter.

Lightning-fast setup that keeps one shared virtual environment ready for temporary tasks.

Use this skill when the user needs Python packages (data processing, scraping, etc.) that are not preinstalled and a full project-specific environment would be overkill. Skip this if the user explicitly wants system Python or a project-local venv.

## Requirements

`uv` available. If missing, you need either `brew` (macOS/Linux) or `curl` to install it.

## Installation

```bash
bash ${baseDir}/install.sh
```

The script will:

- install `uv` via `brew` (macOS/Linux) or the official `curl` installer if `uv` is absent
- create a global uv project at `~/.uv-global`
- create a virtual environment with common packages in `~/.uv-global/.venv`
- create a few useful shims in `~/.uv-global/.venv/bin`

[Optional]prepend the venv bin to your `PATH` so `python` defaults to the global env and shims are available:

```
export PATH=~/.uv-global/.venv/bin:$PATH
```

## Usage

For any quick Python script that needs extra dependencies:

```bash
# install required packages into the global env
uv --project ~/.uv-global add <pkg0> <pkg1> ...

# write your code
touch script.py

# run your script using the global env
uv --project ~/.uv-global run script.py
```

Tips:
- Keep scripts anywhere; the `--project ~/.uv-global` flag ensures they run with the global env.
- Inspect installed packages with `uv --project ~/.uv-global pip list`.
- If a task grows into a real project, switch to a project-local venv instead of this global one.


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
