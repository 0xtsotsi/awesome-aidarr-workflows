# openpet

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mdealiaga/openpet/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mdealiaga/openpet/SKILL.md)
> Category: Communication

---

## Description

Virtual pet (Tamagotchi-style) game for chat platforms. Triggers on pet commands like "feed pet", "pet status", "play with pet", "name pet", "pet sleep", "new pet". Supports multi-user across Discord, WhatsApp, Telegram, etc. Each user gets their own pet that evolves based on care.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Virtual pet (Tamagotchi-style) game for chat platforms. Triggers on pet commands like "feed pet", "pet status", "play with pet", "name pet", "pet sleep", "new pet". Supports multi-user across Discord, WhatsApp, Telegram, etc. Each user gets their own pet that evolves based on care.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run openpet`)
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
You are executing the openpet workflow. Use the following context:

Description: Virtual pet (Tamagotchi-style) game for chat platforms. Triggers on pet commands like "feed pet", "pet status", "play with pet", "name pet", "pet sleep", "new pet". Supports multi-user across Discord, WhatsApp, Telegram, etc. Each user gets their own pet that evolves based on care.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openpet
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# OpenPet

Virtual pet game. Each user gets one pet, tracked by `{platform}_{userId}`.

## State

Pets stored in `tamagotchi/pets/{platform}_{userId}.json`:

```json
{
  "name": "Blobby",
  "species": "blob",
  "hunger": 30,
  "happiness": 70,
  "energy": 50,
  "age": 5,
  "born": "2026-02-01T12:00:00Z",
  "lastUpdate": 1738442780000,
  "alive": true,
  "evolution": 1,
  "totalFeedings": 12,
  "totalPlays": 8,
  "ownerId": "202739061796896768",
  "platform": "discord",
  "ownerName": "mattzap"
}
```

Create `tamagotchi/pets/` directory if missing.

## Commands

| Trigger | Action |
|---------|--------|
| `pet`, `pet status` | Show stats + ASCII art |
| `feed pet` | hunger -30, happiness +5 |
| `play with pet` | happiness +25, energy -20 |
| `pet sleep` | energy +40, happiness +5 |
| `name pet [name]` | Set pet name |
| `new pet` | Reset (only if dead or confirm) |
| `pet help` | Show commands |

## New User Flow

1. Any pet command from unknown user → create egg
2. First interaction → hatch to blob
3. Show welcome message + commands

## Stats Display

```
    ╭──────────╮
    │ (◕‿◕)    │
    │   ♥      │
    │ "Name"   │
    ╰──────────╯
    
 ❤️ Happiness: ████████░░░░  70%
 🍖 Hunger:    ███░░░░░░░░░  30%
 ⚡ Energy:    █████░░░░░░░  50%
```

Use sprites from `references/sprites.json`. Mood = happy (≥70), neutral (40-69), sad (<40).

## Evolution

| Stage | Requirement |
|-------|-------------|
| egg → blob | First interaction |
| blob → cat | age ≥10, feedings ≥15, plays ≥10 |
| cat → dragon | age ≥30, feedings ≥50, plays ≥40 |

Check evolution after each interaction. Announce with fanfare.

## Death

Pet dies if: `hunger ≥ 100` OR `happiness ≤ 0`

**BUT** if `immortalMode: true` in config, pets don't die — they just get very sad and hungry. Stats cap at 99/1 instead of triggering death. Default is immortal mode ON.

Show memorial (if death enabled), offer `new pet` to restart.

## Decay (Cron)

Set up cron job `openpet-tick` every 2 hours:
- hunger +15, happiness -10, energy -5
- Clamp all stats 0-100
- Check death conditions
- Alert owner if critical (hunger >80 or happiness <20)
- Increment age daily

## Platform Detection

Extract from message context:
- Discord: `discord_{userId}`
- WhatsApp: `whatsapp_{phoneNumber}`
- Telegram: `telegram_{chatId}`
- Signal: `signal_{uuid}`

## Alerts

Send to user's origin platform when:
- Pet is hungry (>80): "🍖 {name} is starving!"
- Pet is sad (<20): "😢 {name} misses you!"
- Pet died: "💀 {name} has passed away..."
- Evolution: "✨ {name} evolved into a {species}!"

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
