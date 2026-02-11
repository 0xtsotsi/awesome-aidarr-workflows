# reddit-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/thesethrose/reddit-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/thesethrose/reddit-search/SKILL.md)
> Category: Marketing & Sales

---

## Description

Search Reddit for subreddits and get information about them.

**Homepage:** https://github.com/TheSethRose/clawdbot
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search Reddit for subreddits and get information about them.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run reddit-search`)
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
You are executing the reddit-search workflow. Use the following context:

Description: Search Reddit for subreddits and get information about them.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: reddit-search
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: https://github.com/TheSethRose/clawdbot
```

---

## Original Skill Content



# Reddit Search

Search Reddit for subreddits and get information about them.

## Quick start

```bash
{baseDir}/scripts/reddit-search info programming
{baseDir}/scripts/reddit-search search javascript
{baseDir}/scripts/reddit-search popular 10
{baseDir}/scripts/reddit-search posts typescript 5
```

## Commands

### Get subreddit info

```bash
{baseDir}/scripts/reddit-search info <subreddit>
```

Shows subscriber count, NSFW status, creation date, and description with sidebar links.

### Search for subreddits

```bash
{baseDir}/scripts/reddit-search search <query> [limit]
```

Search for subreddits matching the query. Default limit is 10.

### List popular subreddits

```bash
{baseDir}/scripts/reddit-search popular [limit]
```

List the most popular subreddits. Default limit is 10.

### List new subreddits

```bash
{baseDir}/scripts/reddit-search new [limit]
```

List newly created subreddits. Default limit is 10.

### Get top posts from a subreddit

```bash
{baseDir}/scripts/reddit-search posts <subreddit> [limit]
```

Get the top posts from a subreddit sorted by hot. Default limit is 5.

## Examples

```bash
# Get info about r/programming
{baseDir}/scripts/reddit-search info programming

# Search for JavaScript communities
{baseDir}/scripts/reddit-search search javascript 20

# List top 15 popular subreddits
{baseDir}/scripts/reddit-search popular 15

# List new subreddits
{baseDir}/scripts/reddit-search new 10

# Get top 5 posts from r/typescript
{baseDir}/scripts/reddit-search posts typescript 5
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
