# tiangong-notebooklm-cli

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/fadeloo/tiangong-notebooklm-cli/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/fadeloo/tiangong-notebooklm-cli/SKILL.md)
> Category: Browser & Automation

---

## Description

NotebookLM CLI wrapper via `node {baseDir}/scripts/notebooklm.mjs`. Use for auth, notebooks, chat, sources, notes, sharing, research, and artifact generation/download.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
NotebookLM CLI wrapper via `node {baseDir}/scripts/notebooklm.mjs`. Use for auth, notebooks, chat, sources, notes, sharing, research, and artifact generation/download.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tiangong-notebooklm-cli`)
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
You are executing the tiangong-notebooklm-cli workflow. Use the following context:

Description: NotebookLM CLI wrapper via `node {baseDir}/scripts/notebooklm.mjs`. Use for auth, notebooks, chat, sources, notes, sharing, research, and artifact generation/download.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tiangong-notebooklm-cli
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# NotebookLM CLI Wrapper

## Required parameters
- `node` and `notebooklm` available on PATH.
- NotebookLM CLI authenticated (run `login` if needed).

## Quick start
- Wrapper script: `scripts/notebooklm.mjs` (invokes `notebooklm` CLI).
- Run from the skill directory or use an absolute `{baseDir}` path.

```bash
node {baseDir}/scripts/notebooklm.mjs status
node {baseDir}/scripts/notebooklm.mjs login
node {baseDir}/scripts/notebooklm.mjs list
node {baseDir}/scripts/notebooklm.mjs use <notebook_id>
node {baseDir}/scripts/notebooklm.mjs ask "Summarize the key takeaways" --notebook <notebook_id>
```

## Request & output
- Command form: `node {baseDir}/scripts/notebooklm.mjs <command> [args...]`.
- Prefer `--json` for machine-readable output.
- For long-running tasks, use `--exec-timeout <seconds>`; `--timeout` is reserved for wait/poll commands.

## References
- `references/cli-commands.md`

## Assets
- None.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
