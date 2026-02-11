# geo-ip

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xejrax/geo-ip/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xejrax/geo-ip/SKILL.md)
> Category: Search & Research

---

## Description

Look up geographic location for any IP address

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Look up geographic location for any IP address

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run geo-ip`)
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
You are executing the geo-ip workflow. Use the following context:

Description: Look up geographic location for any IP address

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: geo-ip
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Geo IP

Look up the geographic location for any IP address using the ipinfo.io API. Returns city, region, country, coordinates, and ISP information.

## Commands

```bash
# Look up location for a specific IP address
geo-ip <ip-address>

# Look up your own public IP location
geo-ip me
```

## Install

No installation needed. `curl` is always present on the system. Uses the public ipinfo.io API.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
