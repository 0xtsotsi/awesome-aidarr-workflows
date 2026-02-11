# steam

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mjrussell/steam/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mjrussell/steam/SKILL.md)
> Category: Gaming

---

## Description

Browse, filter, and discover games in a Steam library. Filter by playtime, reviews, Steam Deck compatibility, genres, and tags. Use when user asks about their Steam games, what to play, game recommendations, or Steam Deck compatible games.

**Homepage:** https://github.com/mjrussell/steam-cli
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Browse, filter, and discover games in a Steam library. Filter by playtime, reviews, Steam Deck compatibility, genres, and tags. Use when user asks about their Steam games, what to play, game recommendations, or Steam Deck compatible games.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run steam`)
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
You are executing the steam workflow. Use the following context:

Description: Browse, filter, and discover games in a Steam library. Filter by playtime, reviews, Steam Deck compatibility, genres, and tags. Use when user asks about their Steam games, what to play, game recommendations, or Steam Deck compatible games.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: steam
category: Gaming
version: 1.0.0
user_invocable: True
homepage: https://github.com/mjrussell/steam-cli
```

---

## Original Skill Content



# Steam Games CLI

CLI for browsing and discovering games in your Steam library. Filter by playtime, reviews, Deck compatibility, genres, and tags.

## Installation

```bash
npm install -g steam-games-cli
```

## Setup

1. Get a Steam Web API key from https://steamcommunity.com/dev/apikey
2. Configure the CLI:
```bash
steam config set-key YOUR_API_KEY
steam config set-user YOUR_STEAM_ID
```

## Commands

### Profile

```bash
steam whoami               # Profile info and library stats
steam whoami --json
```

### Library

```bash
steam library              # List all games
steam library --limit 10   # Limit results
steam library --json       # JSON output for scripting
```

### Tags & Genres (Instant)

```bash
steam tags                 # List all 440+ Steam tags
steam tags --json
steam genres               # List all genres
steam genres --json
```

## Filtering Options

### Playtime

```bash
steam library --unplayed                    # Never played
steam library --min-hours 10                # At least 10 hours
steam library --max-hours 5                 # Less than 5 hours
steam library --deck                        # Played on Steam Deck
```

### Reviews (1-9 scale)

```bash
steam library --reviews very-positive       # Exact category
steam library --min-reviews 7               # Score 7+ (Positive and above)
steam library --show-reviews                # Show review column
```

**Categories:** overwhelmingly-positive (9), very-positive (8), positive (7), mostly-positive (6), mixed (5), mostly-negative (4), negative (3), very-negative (2), overwhelmingly-negative (1)

### Steam Deck Compatibility

```bash
steam library --deck-compat verified        # Verified only
steam library --deck-compat playable        # Playable only
steam library --deck-compat ok              # Verified OR Playable
steam library --show-compat                 # Show Deck column
```

### Tags & Genres

```bash
steam library --tag "Roguelike"             # Filter by tag
steam library --genre "Strategy"            # Filter by genre
steam library --show-tags                   # Show tags column
```

### Sorting

```bash
steam library --sort name                   # Alphabetical (default)
steam library --sort playtime               # Most played first
steam library --sort deck                   # Most Deck playtime first
steam library --sort reviews                # Best reviewed first
steam library --sort compat                 # Best Deck compat first
```

## AI Agent Workflow

The CLI is optimized for AI agents with stream fusion and early termination.

### Step 1: Discover available tags/genres (instant)

```bash
steam tags --json
steam genres --json
```

### Step 2: Filter library with combined criteria

```bash
# Unplayed Deck Verified roguelikes with good reviews
steam library --unplayed --deck-compat verified --tag "Roguelike" --min-reviews 7 --limit 10 --json

# Well-reviewed strategy games under 5 hours
steam library --max-hours 5 --genre "Strategy" --min-reviews 8 --limit 5 --json

# Trading games playable on Deck
steam library --tag "Trading" --deck-compat ok --limit 10 --json
```

### Performance Notes

- Local filters (playtime, unplayed) apply first - instant
- Remote filters (reviews, deck compat, tags) fetch in parallel per game
- Early termination: stops when limit is reached
- Use local filters first to minimize API calls

## Usage Examples

**User: "What should I play on my Steam Deck?"**
```bash
steam library --deck-compat verified --min-reviews 7 --sort playtime --limit 10
```

**User: "What roguelikes do I have?"**
```bash
steam library --tag "Roguelike" --show-tags --limit 20
```

**User: "What unplayed games are highly rated?"**
```bash
steam library --unplayed --min-reviews 8 --sort reviews --limit 10 --show-reviews
```

**User: "How many games do I have?"**
```bash
steam whoami
```

**User: "What strategy games work on Deck?"**
```bash
steam library --genre "Strategy" --deck-compat ok --show-compat --limit 15
```

**User: "What tags are available?"**
```bash
steam tags --json
```

## Output Formats

- Default: Colored table
- `--plain`: Plain text list
- `--json`: JSON for scripting/AI agents

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
