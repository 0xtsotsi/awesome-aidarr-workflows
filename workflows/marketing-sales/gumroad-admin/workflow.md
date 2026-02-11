# gumroad-admin

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/abakermi/gumroad-admin/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/abakermi/gumroad-admin/SKILL.md)
> Category: Marketing & Sales

---

## Description

Gumroad Admin CLI. Check sales, products, and manage discounts.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Gumroad Admin CLI. Check sales, products, and manage discounts.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run gumroad-admin`)
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
You are executing the gumroad-admin workflow. Use the following context:

Description: Gumroad Admin CLI. Check sales, products, and manage discounts.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: gumroad-admin
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Gumroad Admin

Manage your Gumroad store from OpenClaw.

## Setup

1. Get your Access Token from Gumroad (Settings > Advanced > Applications).
2. Set it: `export GUMROAD_ACCESS_TOKEN="your_token"`

## Commands

### Sales
```bash
gumroad-admin sales --day today
gumroad-admin sales --last 30
```

### Products
```bash
gumroad-admin products
```

### Discounts
```bash
gumroad-admin discounts create --product <id> --code "TWITTER20" --amount 20 --type percent
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
