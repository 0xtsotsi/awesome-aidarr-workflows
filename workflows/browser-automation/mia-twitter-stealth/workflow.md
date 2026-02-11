# mia-twitter-stealth

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/arubiku/mia-twitter-stealth/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/arubiku/mia-twitter-stealth/SKILL.md)
> Category: Browser & Automation

---

## Description

Twitter/X automation with advanced stealth and anti-detection

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** twitter, automation, stealth, anti-detection, social-media

---

## GOTCHA Framework

### G - Goals
Twitter/X automation with advanced stealth and anti-detection

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run mia-twitter-stealth`)
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
You are executing the mia-twitter-stealth workflow. Use the following context:

Description: Twitter/X automation with advanced stealth and anti-detection

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: mia-twitter-stealth
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Mia Twitter Stealth 🕵️‍♀️

Twitter/X automation with advanced stealth techniques to avoid bot detection.

## Anti-Detection Features

### 1. Playwright Stealth
- Hides `navigator.webdriver`
- Masks Chrome automation flags
- Spoofs plugins and languages

### 2. Headful Mode
- `headless: false` by default
- Real browser UI visible
- Avoids headless detection

### 3. Human Behavior
- Random typing delays (50-150ms)
- Mouse movement simulation
- Random wait times
- Natural scroll patterns

### 4. Session Persistence
- Cookie storage
- LocalStorage persistence
- User data directory

### 5. Cooldown Management
- Rate limit tracking
- Automatic backoff
- 24h cooldown if flagged

## Usage

```bash
# Post tweet
mia-twitter post "Hello world"

# Reply to tweet
mia-twitter reply <tweet-id> "Great post!"

# Like tweets by search
mia-twitter like --search "AI agents" --limit 10

# Follow users
mia-twitter follow --search "founder" --limit 5

# Check notifications
mia-twitter notifications
```

## Safety

- Max 5 actions per hour
- Max 50 per day
- 2-5 min delays between actions
- Human-like patterns only

## Requirements

- X_AUTH_TOKEN env var
- X_CT0 env var
- Playwright with Chromium

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
