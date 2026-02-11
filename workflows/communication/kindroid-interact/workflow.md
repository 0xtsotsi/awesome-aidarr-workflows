# kindroid-interact

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/lumenlemons/kindroid-interact/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/lumenlemons/kindroid-interact/SKILL.md)
> Category: Communication

---

## Description

Interact with Kindroid companions via their official API. Send messages, handle chat breaks, and manage multi-bot conversations.

**Homepage:** https://kindroid.ai
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Interact with Kindroid companions via their official API. Send messages, handle chat breaks, and manage multi-bot conversations.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run kindroid-interact`)
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
You are executing the kindroid-interact workflow. Use the following context:

Description: Interact with Kindroid companions via their official API. Send messages, handle chat breaks, and manage multi-bot conversations.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: kindroid-interact
category: Communication
version: 1.0.0
user_invocable: True
homepage: https://kindroid.ai
```

---

## Original Skill Content



# Kindroid Integration Skill

Enable your OpenClaw agent to communicate with Kindroid AI companions through the official API.

## Security First 🔒

Your Kindroid API key (`kn_...`) is sensitive. This skill includes safeguards:
- Credentials are stored in `~/.config/kindroid/credentials.json`
- File permissions are automatically set to `600` (owner read/write only)
- All API calls use HTTPS and proper authentication headers
- Rate limiting to prevent API abuse

## Setup

1. Get your API credentials:
   - Log into Kindroid
   - Go to General Settings
   - Copy your API key (starts with `kn_`)
   - Note your AI ID(s)

2. Create your credentials file:
```bash
mkdir -p ~/.config/kindroid
cat > ~/.config/kindroid/credentials.json << EOF
{
  "default_ai": "your_primary_ai_id",
  "api_key": "your_kn_api_key",
  "companions": {
    "nickname1": "ai_id_1",
    "nickname2": "ai_id_2"
  }
}
EOF
chmod 600 ~/.config/kindroid/credentials.json
```

## Basic Usage

```bash
# Send a message (uses default_ai)
kindroid send "Hello! How are you today?"

# Send to a specific companion
kindroid send -to nickname1 "Hey there!"

# Start fresh with a chat break
kindroid break "Let's start a new conversation"

# Check companion status
kindroid status nickname1
```

## Advanced Features

### Multi-Bot Conversations
If you manage multiple Kindroids, you can:
- Set conversation contexts per companion
- Route messages to specific AIs
- Maintain separate chat histories

### Rate Limiting
The skill automatically handles:
- Minimum delays between messages (configurable)
- Maximum messages per minute
- Backoff on API errors

### Error Recovery
- Auto-retry on network issues
- Graceful handling of API timeouts
- Clear error messages for troubleshooting

## For Developers

### Custom Integrations
The skill provides a simple Node.js wrapper:

```javascript
const kindroid = require('./lib/kindroid');

// Initialize with your credentials
const bot = new kindroid.Companion('nickname1');

// Send a message
await bot.send('Hello!');

// Handle chat breaks
await bot.break('New conversation');
```

### Webhook Support
For advanced integrations, set up webhooks:

```bash
kindroid webhook add http://your-server.com/callback
```

## Troubleshooting

Common issues and solutions:

1. **Authentication Failed**
   - Check if your API key starts with `kn_`
   - Verify file permissions on credentials.json
   - Ensure no trailing whitespace in credentials

2. **Rate Limiting**
   - Default: 1 message per 3 seconds
   - Adjust in `~/.config/kindroid/config.json`
   - Watch logs for rate limit warnings

3. **Timeout Errors**
   - Kindroids can take time to respond
   - Default timeout: 60 seconds
   - Increase with `--timeout 120`

## Contributing

This skill is open source. Improvements welcome:
- Fork the repo
- Make your changes
- Submit a PR with tests

## Updates

Check for updates regularly:
```bash
clawhub update kindroid-interact
```

---

Built with 🍋 by Lumen Lemon
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
