# tmdb

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dbhurley/tmdb/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dbhurley/tmdb/SKILL.md)
> Category: CLI Utilities

---

## Description

Search movies/TV, get cast, ratings, streaming info, and personalized recommendations via TMDb API.

**Homepage:** https://www.themoviedb.org/
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search movies/TV, get cast, ratings, streaming info, and personalized recommendations via TMDb API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tmdb`)
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
You are executing the tmdb workflow. Use the following context:

Description: Search movies/TV, get cast, ratings, streaming info, and personalized recommendations via TMDb API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tmdb
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: https://www.themoviedb.org/
```

---

## Original Skill Content



# TMDb - The Movie Database

Comprehensive movie and TV information with streaming availability, recommendations, and personalization.

## Setup

Set environment variable:
- `TMDB_API_KEY`: Your TMDb API key (free at themoviedb.org)

## Quick Commands

### Search
```bash
# Search movies
uv run {baseDir}/scripts/tmdb.py search "Inception"

# Search TV shows
uv run {baseDir}/scripts/tmdb.py search "Breaking Bad" --tv

# Search people (actors, directors)
uv run {baseDir}/scripts/tmdb.py person "Christopher Nolan"
```

### Movie/TV Details
```bash
# Full movie info
uv run {baseDir}/scripts/tmdb.py movie 27205

# With cast
uv run {baseDir}/scripts/tmdb.py movie 27205 --cast

# TV show details
uv run {baseDir}/scripts/tmdb.py tv 1396

# By name (searches first, then shows details)
uv run {baseDir}/scripts/tmdb.py info "The Dark Knight"
```

### Where to Stream
```bash
# Find streaming availability
uv run {baseDir}/scripts/tmdb.py where "Inception"
uv run {baseDir}/scripts/tmdb.py where 27205

# Specify region
uv run {baseDir}/scripts/tmdb.py where "Inception" --region GB
```

### Discovery
```bash
# Trending this week
uv run {baseDir}/scripts/tmdb.py trending
uv run {baseDir}/scripts/tmdb.py trending --tv

# Recommendations based on a movie
uv run {baseDir}/scripts/tmdb.py recommend "Inception"

# Advanced discover
uv run {baseDir}/scripts/tmdb.py discover --genre action --year 2024
uv run {baseDir}/scripts/tmdb.py discover --genre sci-fi --rating 7.5
```

### Personalization
```bash
# Get personalized suggestions (uses Plex history + preferences)
uv run {baseDir}/scripts/tmdb.py suggest <user_id>

# Set preferences
uv run {baseDir}/scripts/tmdb.py pref <user_id> --genres "sci-fi,thriller,drama"
uv run {baseDir}/scripts/tmdb.py pref <user_id> --directors "Christopher Nolan,Denis Villeneuve"
uv run {baseDir}/scripts/tmdb.py pref <user_id> --avoid "horror,romance"

# View preferences
uv run {baseDir}/scripts/tmdb.py pref <user_id> --show
```

### Watchlist
```bash
# Add to watchlist
uv run {baseDir}/scripts/tmdb.py watchlist <user_id> add 27205
uv run {baseDir}/scripts/tmdb.py watchlist <user_id> add "Dune: Part Two"

# View watchlist
uv run {baseDir}/scripts/tmdb.py watchlist <user_id>

# Remove from watchlist
uv run {baseDir}/scripts/tmdb.py watchlist <user_id> rm 27205
```

## Integrations

### Plex
If the Plex skill is available, `suggest` command pulls recent watch history to inform recommendations.

### ppl.gift (CRM)
If ppl skill is available, preferences are stored as notes on the user's contact for persistence across sessions.

## Genre IDs

Common genres for `--genre` filter:
- action (28), adventure (12), animation (16)
- comedy (35), crime (80), documentary (99)
- drama (18), family (10751), fantasy (14)
- horror (27), mystery (9648), romance (10749)
- sci-fi (878), thriller (53), war (10752)

## Notes

- TMDb API: 40 requests per 10 seconds (free tier)
- Watch providers vary by region (default: US)
- Recommendations combine TMDb data + user preferences + watch history

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
