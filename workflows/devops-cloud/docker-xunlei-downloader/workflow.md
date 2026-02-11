# docker-xunlei-downloader

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/saaak/docker-xunlei-downloader/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/saaak/docker-xunlei-downloader/SKILL.md)
> Category: DevOps & Cloud

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run docker-xunlei-downloader`)
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
You are executing the docker-xunlei-downloader workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: docker-xunlei-downloader
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Xunlei Docker Downloader Skill

## Description
A skill that allows OpenClaw to interact with Docker-deployed Xunlei services for downloading magnet links and managing download tasks.

## Features
- Detect and submit magnet links to Xunlei Docker service
- Monitor download tasks (in-progress and completed)
- View task status including progress and speed
- Configure Xunlei service connection settings
- **NEW**: Intelligent content filtering to identify and prioritize main content over advertisements

## Configuration
The skill requires the following configuration:
- `xunlei_host`: The host address of the Docker Xunlei service
- `xunlei_port`: The port of the Docker Xunlei service
- `xunlei_ssl`: Whether to use SSL (true/false, default: false)

## Commands
- `xunlei status` - Show current download tasks
- `xunlei submit <magnet_link>` - Submit a magnet link for download (with intelligent content filtering)
- `xunlei submit <magnet_link> --name <task_name>` - Submit with custom task name
- `xunlei config set <host> <port>` - Configure Xunlei service connection
- `xunlei config show` - Show current configuration
- `xunlei completed` - Show completed tasks
- `xunlei version` - Show Xunlei service version

## Intelligent Content Filtering
The skill now includes smart analysis of magnet links to:
- Identify main content vs. advertisement files based on size and filename
- Prioritize large files with content indicators (e.g., "hhd800.com@", "FHD", "1080p")
- Filter out small files with ad indicators (e.g., "game", "demo", "trailer", "合集", "大全")
- Automatically select the most relevant files for download

## Dependencies
- Node.js
- Chrome browser (for authentication methods)

## Implementation Notes
Based on the xunlei-docker-ext project by saaak, this skill provides server-side functionality to interact with Xunlei Docker services without requiring a browser extension.
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
