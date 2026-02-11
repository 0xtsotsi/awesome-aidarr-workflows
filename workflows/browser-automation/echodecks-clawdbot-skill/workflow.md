# echodecks-clawdbot-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/drgeld/echodecks-clawdbot-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/drgeld/echodecks-clawdbot-skill/SKILL.md)
> Category: Browser & Automation

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run echodecks-clawdbot-skill`)
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
You are executing the echodecks-clawdbot-skill workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: echodecks-clawdbot-skill
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# EchoDecks Skill

Integrates with the EchoDecks External API for flashcard management, AI generation, and audio study sessions.

## Configuration
Requires `ECHODECKS_API_KEY` environment variable.

## Tools

### `echodecks_get_user`
Get user profile, credits, and global study statistics.

### `echodecks_list_decks`
List all decks in your account.
- `id` (optional): Retrieve a specific deck by ID.

### `echodecks_create_deck`
Create a new flashcard deck.
- `title` (required): Name of the deck.
- `description` (optional): Brief description.

### `echodecks_list_cards`
List cards in a specific deck.
- `deck_id` (required): The ID of the target deck.

### `echodecks_generate_cards`
Generate new flashcards using AI.
- `deck_id` (required): The target deck ID.
- `topic` (optional): Topic string.
- `text` (optional): Detailed source text.
*Cost: 10 credits.*

### `echodecks_generate_podcast`
Synthesize an audio podcast from a deck.
- `deck_id` (required): The source deck ID.
- `style` (optional): "summary" or "conversation" (default: "summary").
*Cost: 50 credits.*

### `echodecks_podcast_status`
Check the progress of a generated podcast.
- `id` (required): The podcast ID.

### `echodecks_get_study_link`
Get a direct link to a web-based study session.
- `deck_id` (required): The deck to study.

### `echodecks_submit_review`
Submit a spaced-repetition review for a card.
- `card_id` (required): The ID of the card.
- `quality` (required): 0 (Again), 1 (Hard), 2 (Good), 3 (Easy).

## Implementation
All tools wrap the `scripts/echodecks_client.py` CLI.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
