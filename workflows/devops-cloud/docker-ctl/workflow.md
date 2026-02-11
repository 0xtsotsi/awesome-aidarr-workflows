# docker-ctl

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xejrax/docker-ctl/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xejrax/docker-ctl/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Inspect containers, logs, and images via podman

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Inspect containers, logs, and images via podman

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run docker-ctl`)
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
You are executing the docker-ctl workflow. Use the following context:

Description: Inspect containers, logs, and images via podman

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: docker-ctl
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Docker Ctl

Inspect containers, logs, and images via podman. On Bazzite/Fedora, podman is the default container runtime and is always available.

## Commands

```bash
# List running containers
docker-ctl ps

# View container logs
docker-ctl logs <container>

# List local images
docker-ctl images

# Inspect a container
docker-ctl inspect <container>
```

## Install

No installation needed. Bazzite uses `podman` as its container runtime and it is pre-installed.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
