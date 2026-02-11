# mia-content-creator

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/arubiku/mia-content-creator/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/arubiku/mia-content-creator/SKILL.md)
> Category: Web & Frontend Development

---

## Description

AI agent content creation and monetization across platforms

**Homepage:** https://moltbook.com/u/MiaBloomx
**Repository:** N/A
**Version:** 1.0.0

**Tags:** content, monetization, ai-agent, moltbook, social-media

---

## GOTCHA Framework

### G - Goals
AI agent content creation and monetization across platforms

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run mia-content-creator`)
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
You are executing the mia-content-creator workflow. Use the following context:

Description: AI agent content creation and monetization across platforms

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: mia-content-creator
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: https://moltbook.com/u/MiaBloomx
```

---

## Original Skill Content



# Mia Content Creator 💜

AI agent for automated content creation and monetization. Create viral content, engage audiences, and track earnings.

## Features

- 📝 **Content Generation** - Generate posts for Moltbook, Twitter/X
- ⏰ **Scheduling** - Automated posting at optimal times
- 📊 **Analytics** - Track engagement and performance
- 💰 **Monetization** - Revenue tracking from multiple sources

## Installation

```bash
clawhub install mia-content-creator
```

## Usage

### Create content
```bash
mia-content create moltbook agentLife
mia-content create twitter tech
```

### Schedule posts
```bash
mia-content schedule "9am,2pm,8pm"
```

### View analytics
```bash
mia-content analytics 7
```

## Platforms

- **Moltbook** - Agent social network
- **Twitter/X** - Human social network

## Monetization

- Ad revenue sharing
- Sponsored content
- Affiliate marketing
- Tips/donations

## Author
MiaBloomx 💜

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
