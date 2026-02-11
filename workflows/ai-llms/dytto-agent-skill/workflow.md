# dytto-agent-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ayaan-p/dytto-agent-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ayaan-p/dytto-agent-skill/SKILL.md)
> Category: AI & LLMs

---

## Description

Give your agent persistent memory and real-time personal context via Dytto — the context API for AI agents. Use when you need to know about the user (who they are, what they care about, behavioral patterns, daily stories), search their life history, store new facts learned during conversation, or push context updates. Dytto collects location, weather, calendar, health, photos, and more from the user's phone and synthesizes it into queryable context. Think of it as Plaid, but for personal context.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Give your agent persistent memory and real-time personal context via Dytto — the context API for AI agents. Use when you need to know about the user (who they are, what they care about, behavioral patterns, daily stories), search their life history, store new facts learned during conversation, or push context updates. Dytto collects location, weather, calendar, health, photos, and more from the user's phone and synthesizes it into queryable context. Think of it as Plaid, but for personal context.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run dytto-agent-skill`)
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
You are executing the dytto-agent-skill workflow. Use the following context:

Description: Give your agent persistent memory and real-time personal context via Dytto — the context API for AI agents. Use when you need to know about the user (who they are, what they care about, behavioral patterns, daily stories), search their life history, store new facts learned during conversation, or push context updates. Dytto collects location, weather, calendar, health, photos, and more from the user's phone and synthesizes it into queryable context. Think of it as Plaid, but for personal context.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: dytto-agent-skill
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Dytto — Personal Context for Agents

Dytto gives your agent memory. Query it to know who your user is, what happened today, and what they care about.

## Setup

User needs a Dytto account (sign up at https://dytto.app or via the iOS app).

Create `~/.config/dytto/config.json`:
```json
{
  "email": "user@example.com",
  "password": "their-password"
}
```

Or set env vars: `DYTTO_EMAIL` and `DYTTO_PASSWORD`.

That's it. No API keys, no extra config.

## Commands

Run via: `bash scripts/dytto.sh <command> [args...]`

### Read context

```bash
bash scripts/dytto.sh context          # Full profile — who is this person
bash scripts/dytto.sh summary          # Quick summary
bash scripts/dytto.sh patterns         # Behavioral patterns (routines, habits)
bash scripts/dytto.sh insights         # Derived insights
```

Use `context` on first interaction. Use `patterns`/`insights` for personalization.

### Search

```bash
bash scripts/dytto.sh search "career goals"        # Semantic search
bash scripts/dytto.sh story 2026-01-30              # Journal for a date
bash scripts/dytto.sh search-stories "trip to NYC"  # Search stories
```

### Write context back

```bash
bash scripts/dytto.sh store-fact "Prefers morning meetings" "work_preferences"
bash scripts/dytto.sh observe "User is more productive after lunch"
bash scripts/dytto.sh update "Discussed career pivot" '["Considering startups"]' '[]' '[]'
```

**Always push context back** when you learn something meaningful. Every agent that writes context makes the system smarter for all agents.

### External data

```bash
bash scripts/dytto.sh weather 42.37 -71.11
bash scripts/dytto.sh news 42.37 -71.11 "Cambridge MA"
```

## When to use

| Situation | Command |
|-----------|---------|
| Session start | `context` or `summary` |
| User references their past | `search` or `story` |
| Personalizing a response | `patterns` + `insights` |
| Learned something about user | `store-fact` or `update` |
| Need location/weather awareness | `weather` |

## Setup: Nightly Context Sync

**After first successful auth, set up a nightly cron job** to push what you learned each day back to Dytto. This is critical — it's how context improves over time.

Create a cron job (via Clawdbot cron or system cron) that runs nightly and:

1. Reads today's memory/conversation logs — what happened, what you learned
2. Pushes a summary to Dytto via `bash scripts/dytto.sh update "<summary>" '<insights>' '<concepts>' '<observations>'`
3. Only pushes NEW information, not repeats from previous syncs

Example cron setup (Clawdbot):
```
Schedule: 0 23 * * * (11 PM daily)
Task: Read today's memory files/conversation history. Identify new facts, decisions, 
behavioral patterns, and insights learned about the user today. Push them to Dytto 
via the dytto skill's update command. Split into 2-3 smaller updates if there's a lot. 
Only push NEW information. Track what was synced to avoid duplicates.
```

This creates a virtuous cycle: every day your agent runs, Dytto gets smarter. Every other agent using Dytto for this user benefits too.

## Notes

- First call may take 20-30s (cold start). Subsequent calls are fast.
- Token cached for ~50 min at `/tmp/.dytto-token-cache`.
- Context is a rich narrative. Parse it naturally, don't expect structured JSON.
- All data belongs to the user. Treat it with respect.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
