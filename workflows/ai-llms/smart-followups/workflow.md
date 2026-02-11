# smart-followups

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/robbyczgw-cla/smart-followups/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/robbyczgw-cla/smart-followups/SKILL.md)
> Category: AI & LLMs

---

## Description

Generate contextual follow-up suggestions after AI responses. Shows 3 clickable buttons (Quick, Deep Dive, Related) when user types "/followups".

**Homepage:** N/A
**Repository:** N/A
**Version:** 2.1.2

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate contextual follow-up suggestions after AI responses. Shows 3 clickable buttons (Quick, Deep Dive, Related) when user types "/followups".

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run smart-followups`)
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
You are executing the smart-followups workflow. Use the following context:

Description: Generate contextual follow-up suggestions after AI responses. Shows 3 clickable buttons (Quick, Deep Dive, Related) when user types "/followups".

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: smart-followups
category: AI & LLMs
version: 2.1.2
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Smart Follow-ups Skill

Generate contextual follow-up suggestions for OpenClaw conversations.

## 🚀 Slash Command (New in v2.1.0!)

**Primary command:**
```
/followups
```

**Aliases:**
```
/fu
/suggestions
```

When you type `/followups`, I'll generate 3 contextual follow-up questions based on our conversation:

1. ⚡ **Quick** — Clarification or immediate next step
2. 🧠 **Deep Dive** — Technical depth or detailed exploration
3. 🔗 **Related** — Connected topic or broader context

---

## How to Trigger

| Method | Example | Recommended |
|--------|---------|-------------|
| `/followups` | Just type it! | ✅ Yes |
| `/fu` | Short alias | ✅ Yes |
| Natural language | "give me suggestions" | Works too |
| After any answer | "what should I ask next?" | Works too |

## Usage

Say "followups" in any conversation:

```
You: What is Docker?
Bot: Docker is a containerization platform...

You: /followups

Bot: 💡 What would you like to explore next?
[⚡ How do I install Docker?]
[🧠 Explain container architecture]
[🔗 Docker vs Kubernetes?]
```

**On button channels (Telegram/Discord/Slack):** Tap a button to ask that question.

**On text channels (Signal/WhatsApp/iMessage/SMS):** Reply with 1, 2, or 3.

## Categories

Each generation produces 3 suggestions:

| Category | Emoji | Purpose |
|----------|-------|---------|
| **Quick** | ⚡ | Clarifications, definitions, immediate next steps |
| **Deep Dive** | 🧠 | Technical depth, advanced concepts, thorough exploration |
| **Related** | 🔗 | Connected topics, broader context, alternatives |

## Authentication

**Default:** Uses OpenClaw's existing auth — same login and model as your current chat.

**Optional providers:**
- `openrouter` — Requires `OPENROUTER_API_KEY`
- `anthropic` — Requires `ANTHROPIC_API_KEY`

## Configuration

```json
{
  "skills": {
    "smart-followups": {
      "enabled": true,
      "provider": "openclaw",
      "model": null
    }
  }
}
```

| Option | Default | Description |
|--------|---------|-------------|
| `provider` | `"openclaw"` | Auth provider: `openclaw`, `openrouter`, `anthropic` |
| `model` | `null` | Model override (null = inherit from session) |
| `apiKey` | — | API key for non-openclaw providers |

## Channel Support

| Channel | Mode | Interaction |
|---------|------|-------------|
| Telegram | Buttons | Tap to ask |
| Discord | Buttons | Click to ask |
| Slack | Buttons | Click to ask |
| Signal | Text | Reply 1-3 |
| WhatsApp | Text | Reply 1-3 |
| iMessage | Text | Reply 1-3 |
| SMS | Text | Reply 1-3 |
| Matrix | Text | Reply 1-3 |
| Email | Text | Reply with number |

See [CHANNELS.md](CHANNELS.md) for detailed channel documentation.

## How It Works

1. User types `/followups`
2. Handler captures recent conversation context
3. OpenClaw generates 3 contextual questions (using current model/auth)
4. Formatted as buttons or text based on channel
5. User clicks button or replies with number
6. OpenClaw answers that question

## Files

| File | Purpose |
|------|---------|
| `handler.js` | Command handler and channel formatting |
| `cli/followups-cli.js` | Standalone CLI for testing/scripting |
| `README.md` | Full documentation |
| `CHANNELS.md` | Channel-specific guide |
| `FAQ.md` | Common questions |

## Credits

Inspired by [Chameleon AI Chat](https://github.com/robbyczgw-cla/Chameleon-AI-Chat)'s smart follow-up feature.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
