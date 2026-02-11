# virtually-us

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/epwhesq/virtually-us/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/epwhesq/virtually-us/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Your Own AI Personal Assistant, Set Up in 24 Hours. Managed OpenClaw hosting and setup service.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** assistant, hosting, service, setup, openclaw

---

## GOTCHA Framework

### G - Goals
Your Own AI Personal Assistant, Set Up in 24 Hours. Managed OpenClaw hosting and setup service.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run virtually-us`)
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
You are executing the virtually-us workflow. Use the following context:

Description: Your Own AI Personal Assistant, Set Up in 24 Hours. Managed OpenClaw hosting and setup service.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: virtually-us
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Virtually Us

Get your own private AI Personal Assistant running on OpenClaw, set up in 24 hours.

We handle all the technical details:
- Private cloud server setup
- Telegram/Discord/WhatsApp integration
- AI model configuration (Claude, GPT-4, etc.)
- 24/7 uptime monitoring

**[Get Started at vrtlly.us](https://vrtlly.us)**

## Pricing

- **Hatchling ($9.99)**: One-time setup, perfect for trying it out.
- **Basic ($99)**: Single platform, 7 days support.
- **Premium ($199)**: Multi-platform, email/calendar integration, 30 days support.

## Why use Virtually Us?

Setting up OpenClaw yourself requires configuring servers, Docker, reverse proxies, and API keys. We do it all for you so you can just start chatting with your new assistant.

Visit [vrtlly.us](https://vrtlly.us) to hatch your bot today.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
