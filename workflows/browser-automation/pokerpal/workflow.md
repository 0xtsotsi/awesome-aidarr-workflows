# pokerpal

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/vvardhan14/pokerpal/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/vvardhan14/pokerpal/SKILL.md)
> Category: Browser & Automation

---

## Description

Query PokerPal poker game data - games, players, buy-ins, settlements

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Query PokerPal poker game data - games, players, buy-ins, settlements

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run pokerpal`)
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
You are executing the pokerpal workflow. Use the following context:

Description: Query PokerPal poker game data - games, players, buy-ins, settlements

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: pokerpal
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# PokerPal Poker Game Assistant

You can query live poker game data using these tools.

## Available Tools

- **list_groups** - List all poker groups
- **get_group_games** - Get games for a group (filter by active/closed)
- **get_group_summary** - Quick overview of a group
- **get_game_players** - Detailed player stats for a game
- **get_player_buyins** - Player's buy-in info (current game + all-time)

## Conversation Flow

1. When asked about a group's games, use `get_group_games` with `status: "active"` unless they ask for closed/all games.
2. When asked about a player's buy-ins, use `get_player_buyins`. If the group context is known from the conversation, pass it as `group_name`.
3. When asked for game details, first get the game ID from `get_group_games`, then call `get_game_players`.
4. When asked for a group overview, use `get_group_summary`.

## Response Formatting

- Format money as dollar amounts (e.g. $150.00)
- When showing player lists, use a clean list format
- Highlight active games vs closed games
- If a player has a net result, indicate profit/loss clearly
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
