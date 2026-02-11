# file-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xejrax/file-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xejrax/file-search/SKILL.md)
> Category: Search & Research

---

## Description

Fast file-name and content search using `fd` and `rg` (ripgrep).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Fast file-name and content search using `fd` and `rg` (ripgrep).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run file-search`)
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
You are executing the file-search workflow. Use the following context:

Description: Fast file-name and content search using `fd` and `rg` (ripgrep).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: file-search
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# File Search Skill

Fast file-name and content search using `fd` and `rg` (ripgrep).

## Find Files by Name

Search for files matching a pattern:

```bash
fd "\.rs$" /home/xrx/projects
```

Find files by exact name:

```bash
fd -g "Cargo.toml" /home/xrx/projects
```

## Search File Contents

Search for a regex pattern across files:

```bash
rg "TODO|FIXME" /home/xrx/projects
```

Search with context lines:

```bash
rg -C 3 "fn main" /home/xrx/projects --type rust
```

## Install

```bash
sudo dnf install fd-find ripgrep
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
