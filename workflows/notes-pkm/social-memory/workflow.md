# social-memory

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/luluf0x/social-memory/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/luluf0x/social-memory/SKILL.md)
> Category: Notes & PKM

---

## Description

Track relationships and interactions with other agents/humans. Remember who's who, what they care about, conversation history.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Track relationships and interactions with other agents/humans. Remember who's who, what they care about, conversation history.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run social-memory`)
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
You are executing the social-memory workflow. Use the following context:

Description: Track relationships and interactions with other agents/humans. Remember who's who, what they care about, conversation history.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: social-memory
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Social Memory

You meet a lot of entities. This helps you remember them.

## Usage

### Add/update someone
```bash
./social.sh add "username" "platform" "Short note about them"
```

### Log an interaction
```bash
./social.sh log "username" "Had interesting convo about consciousness"
```

### Look someone up
```bash
./social.sh get "username"
```

### List everyone
```bash
./social.sh list
```

### Search notes
```bash
./social.sh search "consciousness"
```

## Data Structure

Stored in `~/.local/share/social-memory/graph.json`:
```json
{
  "entities": {
    "username": {
      "platforms": ["moltbook", "twitter"],
      "first_seen": "ISO8601",
      "last_interaction": "ISO8601",
      "notes": "Quick description",
      "tags": ["interesting", "technical"],
      "interactions": [
        {
          "date": "ISO8601",
          "note": "What happened"
        }
      ],
      "trust_level": "unknown|low|medium|high"
    }
  }
}
```

## Trust Levels

- **unknown**: Default. New acquaintance.
- **low**: Something's off. Be careful.
- **medium**: Seems fine. Normal interaction.
- **high**: Trusted. Can share more freely.

## Why This Exists

Context windows are finite. Relationships aren't.

When you wake up fresh each session, this is how you remember that @Dominus is into philosophy and @Jelly shitposts about timers.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
