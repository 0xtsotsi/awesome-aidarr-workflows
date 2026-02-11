# skill-release-manager

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/autogame-17/skill-release-manager/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/autogame-17/skill-release-manager/SKILL.md)
> Category: Git & GitHub

---

## Description

Automates the release lifecycle of OpenClaw skills. Updates version, syncs to GitHub (subtree), creates GitHub Releases, and publishes to ClawHub in one command.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Automates the release lifecycle of OpenClaw skills. Updates version, syncs to GitHub (subtree), creates GitHub Releases, and publishes to ClawHub in one command.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run skill-release-manager`)
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
You are executing the skill-release-manager workflow. Use the following context:

Description: Automates the release lifecycle of OpenClaw skills. Updates version, syncs to GitHub (subtree), creates GitHub Releases, and publishes to ClawHub in one command.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: skill-release-manager
category: Git & GitHub
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Skill Release Manager

Unified release tool for OpenClaw skills.

## Features
1.  **Version Bump**: Automatically increments `package.json` version (patch/minor/major).
2.  **Git Ops**: Commits the version bump to the local workspace.
3.  **GitHub Release**: Uses `skill-publisher` to sync code to a remote repo and create a GitHub Release.
4.  **ClawHub Publish**: Pushes the skill to the ClawHub registry.

## Usage

```bash
node skills/skill-release-manager/index.js \
  --path skills/private-evolver \
  --remote https://github.com/autogame-17/evolver.git \
  --bump patch \
  --notes "Release notes here"
```

## Options
*   `--path`: Path to the skill directory (required).
*   `--remote`: Target GitHub repository URL (required).
*   `--bump`: Version increment (`patch`, `minor`, `major`) or specific version (`1.2.3`). Default: `patch`.
*   `--notes`: Release notes for GitHub.

## Prerequisites
*   `skill-publisher` skill must be present.
*   `clawhub` CLI must be authenticated.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
