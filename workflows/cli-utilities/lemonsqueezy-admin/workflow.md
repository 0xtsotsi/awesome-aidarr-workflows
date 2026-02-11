# lemonsqueezy-admin

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/abakermi/lemonsqueezy-admin/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/abakermi/lemonsqueezy-admin/SKILL.md)
> Category: CLI Utilities

---

## Description

Admin CLI for Lemon Squeezy stores. View orders, subscriptions, and customers.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Admin CLI for Lemon Squeezy stores. View orders, subscriptions, and customers.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run lemonsqueezy-admin`)
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
You are executing the lemonsqueezy-admin workflow. Use the following context:

Description: Admin CLI for Lemon Squeezy stores. View orders, subscriptions, and customers.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: lemonsqueezy-admin
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Lemon Squeezy Admin 🍋

Manage your Lemon Squeezy store from the command line.

## Setup

1. Get an API Key from [Lemon Squeezy Settings > API](https://app.lemonsqueezy.com/settings/api).
2. Set it: `export LEMONSQUEEZY_API_KEY="your_key"`

## Commands

### Orders
```bash
ls-admin orders --limit 10
# Output: #1234 - $49.00 - john@example.com (Paid)
```

### Subscriptions
```bash
ls-admin subscriptions
# Output: Active: 15 | MMR: $450
```

### Stores
```bash
ls-admin stores
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
