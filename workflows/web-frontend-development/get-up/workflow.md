# get-up

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/qidu/get-up/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/qidu/get-up/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Get current public IP address and geolocation information. Use when users ask about IP addresses, network location, or want to check their public IP. Supports both fetching IP info and displaying it clearly.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Get current public IP address and geolocation information. Use when users ask about IP addresses, network location, or want to check their public IP. Supports both fetching IP info and displaying it clearly.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run get-up`)
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
You are executing the get-up workflow. Use the following context:

Description: Get current public IP address and geolocation information. Use when users ask about IP addresses, network location, or want to check their public IP. Supports both fetching IP info and displaying it clearly.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: get-up
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# IP Lookup Skill

## Overview

This skill provides a simple way to check your public IP address and its geolocation information.

## Usage

When users ask:
- "What is my IP?"
- "What is my current IP address?"
- "Where am I located?"
- "Check my IP location"
- "What's my public IP?"
- "What's the IP?"
- "What's your IP?"

Execute the workflow below.

## Workflow

### Basic IP Check

Run this command to get your public IP and location:

```bash
curl -s myip.ipip.net
```

Example output:
```
Current IP：8.8.8.8  From: SF CA USA Google
Current IP：1.1.1.1  From: SF CA USA Cloudflare
```

### Alternative Methods

If the above fails, try these alternatives:

**Method 1: icanhazip.com (fallback)**
```bash
curl -s icanhazip.com
```

**Method 2: ipify API**
```bash
curl -s https://api.ipify.org
```

**Method 3: ifconfig.me**
```bash
curl -s ifconfig.me
```

### Full Geolocation Lookup

For more detailed geolocation info:

```bash
curl -s https://ipinfo.io/$(curl -s https://api.ipify.org)/json
```

## Display Format

Present the information clearly:

**IP Address:** [address]
**Location:** [city], [region], [country]
**ISP:** [ISP name]
**Org:** [organization]

## Error Handling

If the primary service (`myip.ipip.net`) fails:
1. Try alternative services one by one
2. Report which service succeeded
3. If all fail, inform the user about the network issue

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
