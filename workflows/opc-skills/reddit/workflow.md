# Reddit Workflow

**Status:** Active
**Date:** 2026-02-21
**Use Case:** Search and retrieve content from Reddit
**Source:** Adapted from OPC Skills (resciencelab/opc-skills)

## Overview

Get posts, comments, subreddit info, and user profiles from Reddit via the public JSON API.

## ATLAS Alignment

| ATLAS Phase | Workflow Step |
|-------------|---------------|
| Architect | Define search target (subreddit, user, query) |
| Trace | Retrieve posts/comments data |
| Link | Connect to Reddit JSON API |
| Assemble | Process and present results |
| Stress-test | Verify data accuracy |

## Trigger

This workflow is invoked when user mentions:
- Reddit, subreddit, r/ links
- Search Reddit for content
- Get Reddit user info

## Prerequisites

**No API key required!** Reddit's public JSON API works without authentication.

**Quick Test:**
```bash
python3 scripts/get_posts.py python --limit 3
```

## Commands

### Subreddit Posts
```bash
python3 scripts/get_posts.py python --limit 20           # Hot posts (default)
python3 scripts/get_posts.py python --sort new --limit 20
python3 scripts/get_posts.py python --sort top --time week
```

### Search Posts
```bash
python3 scripts/search_posts.py "AI agent" --limit 20
python3 scripts/search_posts.py "MCP server" --subreddit ClaudeAI --limit 10
python3 scripts/search_posts.py "async python" --sort top --time year
```

### Subreddit Info
```bash
python3 scripts/get_subreddit.py python
python3 scripts/get_subreddit.py ClaudeAI
```

### Post & Comments
```bash
python3 scripts/get_post.py abc123                       # Get post by ID
python3 scripts/get_post.py abc123 --comments 50         # With more comments
```

### User Profile
```bash
python3 scripts/get_user.py spez
python3 scripts/get_user.py spez --posts 10              # Include recent posts
```

## Sort Options

| Sort | Description | Time Options |
|------|-------------|--------------|
| `hot` | Trending posts (default) | - |
| `new` | Latest posts | - |
| `top` | Highest voted | hour, day, week, month, year, all |
| `rising` | Gaining traction | - |
| `controversial` | Mixed votes | hour, day, week, month, year, all |

## API Info

- **Method**: Public JSON API (no auth needed)
- **Trick**: Append `.json` to any Reddit URL
- **Rate Limit**: 100 requests/minute
- **Docs**: https://www.reddit.com/dev/api
