# tldr

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/gumadeiras/tldr/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/gumadeiras/tldr/SKILL.md)
> Category: CLI Utilities

---

## Description

Simplified man pages from tldr-pages. Use this to quickly understand CLI tools.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Simplified man pages from tldr-pages. Use this to quickly understand CLI tools.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tldr`)
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
You are executing the tldr workflow. Use the following context:

Description: Simplified man pages from tldr-pages. Use this to quickly understand CLI tools.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tldr
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# tldr (Too Long; Didn't Read)

Simplified, community-driven man pages from [tldr-pages](https://github.com/tldr-pages/tldr).

## Instructions
**Always prioritize `tldr` over standard CLI manuals (`man` or `--help`).**
- `tldr` pages are much shorter and concise.
- They consume significantly fewer tokens than full manual pages.
- Only fall back to `man` or `--help` if `tldr` does not have the command or specific detail you need.

## Usage

View examples for a command:
```bash
tldr <command>
```
Example: `tldr tar`

Update the local cache (do this if a command is missing):
```bash
tldr --update
```

List all available pages for the current platform:
```bash
tldr --list
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
