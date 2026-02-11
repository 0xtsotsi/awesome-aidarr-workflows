# openclaw-postsyncer

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/abakermi/openclaw-postsyncer/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/abakermi/openclaw-postsyncer/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Manage your PostSyncer social media workflows.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage your PostSyncer social media workflows.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run openclaw-postsyncer`)
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
You are executing the openclaw-postsyncer workflow. Use the following context:

Description: Manage your PostSyncer social media workflows.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openclaw-postsyncer
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# PostSyncer Skill

Automate your social media scheduling with PostSyncer.

## Setup

1. Get your API Key from [PostSyncer Settings](https://app.postsyncer.com/settings).
2. Set it: `export POSTSYNCER_API_KEY="your_key"`

## Commands

### Workspaces
List your workspaces.

```bash
postsyncer workspaces
```

### Posts
List your scheduled/published posts.

```bash
postsyncer posts
```

### Create Post
(Basic text post)

```bash
postsyncer create-post -w <workspace_id> -t "Hello world"
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
