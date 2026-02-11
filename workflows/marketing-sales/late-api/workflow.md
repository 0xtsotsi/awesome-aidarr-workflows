# late-api

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mikipalet/late-api/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mikipalet/late-api/SKILL.md)
> Category: Marketing & Sales

---

## Description

Official Late API reference for scheduling posts across 13 social media platforms. Covers authentication, endpoints, webhooks, and platform-specific features. Use when building with the Late Social Media Scheduling API.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Official Late API reference for scheduling posts across 13 social media platforms. Covers authentication, endpoints, webhooks, and platform-specific features. Use when building with the Late Social Media Scheduling API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run late-api`)
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
You are executing the late-api workflow. Use the following context:

Description: Official Late API reference for scheduling posts across 13 social media platforms. Covers authentication, endpoints, webhooks, and platform-specific features. Use when building with the Late Social Media Scheduling API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: late-api
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Late API Reference

Schedule posts across 13 social media platforms with a single API.

**Base URL:** `https://getlate.dev/api/v1`

**Docs:** [getlate.dev/docs](https://getlate.dev/docs)

## Quick Start

```bash
# 1. Create profile
curl -X POST https://getlate.dev/api/v1/profiles \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{"name": "My Brand"}'

# 2. Connect account (opens OAuth)
curl "https://getlate.dev/api/v1/connect/twitter?profileId=PROFILE_ID" \
  -H "Authorization: Bearer YOUR_API_KEY"

# 3. Create post
curl -X POST https://getlate.dev/api/v1/posts \
  -H "Authorization: Bearer YOUR_API_KEY" \
  -d '{"content": "Hello!", "platforms": [{"platform": "twitter", "accountId": "ACC_ID"}], "publishNow": true}'
```

## Rule Files

Read individual rule files for detailed documentation:

- [rules/authentication.md](rules/authentication.md) - API key format, usage examples, core concepts
- [rules/posts.md](rules/posts.md) - Create, schedule, retry posts, bulk upload
- [rules/accounts.md](rules/accounts.md) - List accounts, health checks, follower stats
- [rules/connect.md](rules/connect.md) - OAuth flows, Bluesky app password, Telegram bot token
- [rules/platforms.md](rules/platforms.md) - Platform-specific data for all 13 platforms
- [rules/webhooks.md](rules/webhooks.md) - Configure webhooks, verify signatures, events
- [rules/media.md](rules/media.md) - Presigned uploads, supported formats, platform limits
- [rules/queue.md](rules/queue.md) - Queue management, slots configuration
- [rules/analytics.md](rules/analytics.md) - YouTube daily views, LinkedIn analytics
- [rules/tools.md](rules/tools.md) - Media download, hashtag checker, transcripts
- [rules/errors.md](rules/errors.md) - Error codes, rate limits, publishing logs
- [rules/sdks.md](rules/sdks.md) - Direct API usage examples

## Supported Platforms

Twitter/X, Instagram, Facebook, LinkedIn, TikTok, YouTube, Pinterest, Reddit, Bluesky, Threads, Google Business, Telegram, Snapchat

---

*[Late](https://getlate.dev) - Social Media Scheduling API for Developers*

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
