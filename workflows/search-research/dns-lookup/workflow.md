# dns-lookup

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xejrax/dns-lookup/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xejrax/dns-lookup/SKILL.md)
> Category: Search & Research

---

## Description

Resolve hostnames to IP addresses using `dig` from bind-utils.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Resolve hostnames to IP addresses using `dig` from bind-utils.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run dns-lookup`)
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
You are executing the dns-lookup workflow. Use the following context:

Description: Resolve hostnames to IP addresses using `dig` from bind-utils.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: dns-lookup
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# DNS Lookup Skill

Resolve hostnames to IP addresses using `dig`. Provided by the `bind-utils` package.

## Basic Lookup

Resolve A records for a hostname:

```bash
dig example.com A +short
```

## IPv6 Lookup

Resolve AAAA records:

```bash
dig example.com AAAA +short
```

## Full DNS Record

Get the full DNS response with authority and additional sections:

```bash
dig example.com ANY
```

## Reverse Lookup

Find the hostname for an IP address:

```bash
dig -x 93.184.216.34 +short
```

## Install

```bash
sudo dnf install bind-utils
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
