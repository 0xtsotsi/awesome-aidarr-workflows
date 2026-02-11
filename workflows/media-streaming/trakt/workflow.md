# trakt

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mjrussell/trakt/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mjrussell/trakt/SKILL.md)
> Category: Media & Streaming

---

## Description

Track and view your watched movies and TV shows via trakt.tv. Use when user asks about their watch history, what they've been watching, or wants to search for movies/shows.

**Homepage:** https://trakt.tv
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Track and view your watched movies and TV shows via trakt.tv. Use when user asks about their watch history, what they've been watching, or wants to search for movies/shows.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run trakt`)
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
You are executing the trakt workflow. Use the following context:

Description: Track and view your watched movies and TV shows via trakt.tv. Use when user asks about their watch history, what they've been watching, or wants to search for movies/shows.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: trakt
category: Media & Streaming
version: 1.0.0
user_invocable: True
homepage: https://trakt.tv
```

---

## Original Skill Content



# Trakt CLI

Query your trakt.tv watch history and search for movies/TV shows.

## Installation

```bash
npm install -g trakt-cli
```

## Setup

1. Create an app at https://trakt.tv/oauth/applications/new
2. Run: `trakt-cli auth --client-id <id> --client-secret <secret>`
3. Visit the URL shown and enter the device code
4. Credentials saved to `~/.trakt.yaml`

## Commands

### Watch History

```bash
trakt-cli history                  # Recent history (default: 10 items)
trakt-cli history --limit 25       # Show more
trakt-cli history --page 2         # Paginate
```

### Search

```bash
trakt-cli search "Breaking Bad"
trakt-cli search "The Matrix"
```

## Usage Examples

**User: "What have I been watching lately?"**
```bash
trakt-cli history
```

**User: "Show me my last 20 watched items"**
```bash
trakt-cli history --limit 20
```

**User: "Find info about Severance"**
```bash
trakt-cli search "Severance"
```

## Notes

- Search works without authentication
- History requires authentication
- Read-only access to watch history

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
