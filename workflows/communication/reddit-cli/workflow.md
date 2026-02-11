# reddit-cli

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kelsia14/reddit-cli/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kelsia14/reddit-cli/SKILL.md)
> Category: Communication

---

## Description

Reddit CLI using cookies for authentication. Read posts, search, and get subreddit info.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.2

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Reddit CLI using cookies for authentication. Read posts, search, and get subreddit info.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run reddit-cli`)
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
You are executing the reddit-cli workflow. Use the following context:

Description: Reddit CLI using cookies for authentication. Read posts, search, and get subreddit info.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: reddit-cli
category: Communication
version: 1.0.2
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Reddit CLI

Read Reddit using your session cookies. No API key needed.

## Quick start

```bash
reddit-cli posts programming 10       # Get 10 hot posts
reddit-cli posts gaming 5 top         # Get top 5 posts
reddit-cli search "python tutorial"   # Search all Reddit
reddit-cli search "help" --sub linux  # Search in subreddit
reddit-cli info AskReddit             # Subreddit info
reddit-cli check                      # Test connection
```

## Commands

### Get posts from subreddit
```bash
reddit-cli posts <subreddit> [limit] [sort]
```
- limit: number of posts (default: 10)
- sort: hot, new, top, rising (default: hot)

### Search Reddit
```bash
reddit-cli search <query> [--sub <subreddit>] [limit]
```

### Get subreddit info
```bash
reddit-cli info <subreddit>
```

### Check connection
```bash
reddit-cli check
```

## Environment

Set these in `~/.bashrc`:
```bash
export REDDIT_SESSION="your_reddit_session_cookie"
export TOKEN_V2="your_token_v2_cookie"  # optional
```

## Getting cookies

1. Go to reddit.com (logged in)
2. DevTools (F12) → Application → Cookies → reddit.com
3. Copy `reddit_session` value
4. Optionally copy `token_v2` value

## Notes

- Cookies expire, you may need to refresh them periodically
- Respects Reddit's rate limits
- For personal use only

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
