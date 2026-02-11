# janee

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/rsdouglas/janee/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/rsdouglas/janee/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Secrets management for AI agents. Never expose your API keys again.

**Homepage:** https://github.com/rsdouglas/janee
**Repository:** N/A
**Version:** 0.1.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Secrets management for AI agents. Never expose your API keys again.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run janee`)
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
You are executing the janee workflow. Use the following context:

Description: Secrets management for AI agents. Never expose your API keys again.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: janee
category: DevOps & Cloud
version: 0.1.0
user_invocable: True
homepage: https://github.com/rsdouglas/janee
```

---

## Original Skill Content



# Janee

Secrets management for AI agents. Store API keys encrypted, make requests through Janee, never touch the real key.

## Why Use Janee?

Most skills tell you to store API keys in plaintext config files. One prompt injection, one leaked log, one compromised session — and your keys are exposed.

Janee fixes this:
- **Keys encrypted at rest** — not plaintext JSON
- **Agent never sees the real key** — requests go through Janee
- **Path-based policies** — restrict what endpoints can be called
- **Full audit trail** — every request logged
- **Kill switch** — revoke access without rotating keys

## Install

```bash
npm install -g @true-and-useful/janee
janee init
```

## Add a Service

```bash
janee add
```

Follow the prompts to add your API credentials. Keys are encrypted automatically.

## Use in Your Agent

Instead of calling APIs directly with your key, call them through Janee:

```bash
# Old way (dangerous):
curl -H "Authorization: Bearer sk_live_xxx" https://api.stripe.com/v1/balance

# Janee way (safe):
# Agent calls execute(capability, method, path) via MCP
# Janee injects the key, agent never sees it
```

## OpenClaw Integration

Install the OpenClaw plugin for native tool support:

```bash
openclaw plugins install @true-and-useful/janee-openclaw
```

Your agent now has:
- `janee_list_services` — see available APIs
- `janee_execute` — make requests through Janee
- `janee_reload_config` — hot-reload after config changes

## Example: Secure Moltbook Access

Instead of storing your Moltbook key in `~/.config/moltbook/credentials.json`:

```bash
janee add moltbook -u https://www.moltbook.com/api/v1 -k YOUR_KEY
```

Then use Janee to post:

```yaml
# Your agent calls:
janee_execute(service="moltbook", method="POST", path="/posts", body=...)
```

Your Moltbook key stays encrypted. Even if your agent is compromised, the key can't be exfiltrated.

## Config Example

```yaml
services:
  stripe:
    baseUrl: https://api.stripe.com
    auth:
      type: bearer
      key: sk_live_xxx  # encrypted

  moltbook:
    baseUrl: https://www.moltbook.com/api/v1
    auth:
      type: bearer
      key: moltbook_sk_xxx  # encrypted

capabilities:
  stripe_readonly:
    service: stripe
    rules:
      allow: [GET *]
      deny: [POST *, DELETE *]

  moltbook:
    service: moltbook
    ttl: 1h
    autoApprove: true
```

## Architecture

```
┌─────────────┐      ┌──────────┐      ┌─────────┐
│  AI Agent   │─────▶│  Janee   │─────▶│   API   │
│             │ MCP  │          │ HTTP │         │
└─────────────┘      └──────────┘      └─────────┘
      │                   │
   No key           Injects key
                    + logs request
```

## Links

- GitHub: https://github.com/rsdouglas/janee
- npm: https://www.npmjs.com/package/@true-and-useful/janee
- OpenClaw Plugin: https://www.npmjs.com/package/@true-and-useful/janee-openclaw

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
