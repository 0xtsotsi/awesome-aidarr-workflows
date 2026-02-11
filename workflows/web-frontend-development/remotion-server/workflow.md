# remotion-server

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mvanhorn/remotion-server/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mvanhorn/remotion-server/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Headless video rendering with Remotion. Works on any Linux server - no Mac or GUI needed. Templates for chat demos, promos, and more.

**Homepage:** https://remotion.dev
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Headless video rendering with Remotion. Works on any Linux server - no Mac or GUI needed. Templates for chat demos, promos, and more.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run remotion-server`)
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
You are executing the remotion-server workflow. Use the following context:

Description: Headless video rendering with Remotion. Works on any Linux server - no Mac or GUI needed. Templates for chat demos, promos, and more.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: remotion-server
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: https://remotion.dev
```

---

## Original Skill Content



# Remotion Server

Render videos headlessly on any Linux server using Remotion. No Mac or GUI required.

## Setup (one-time)

Install browser dependencies:
```bash
bash {baseDir}/scripts/setup.sh
```

## Quick Start

### Create a project:
```bash
bash {baseDir}/scripts/create.sh my-video
cd my-video
```

### Render a video:
```bash
npx remotion render MyComp out/video.mp4
```

## Templates

### Chat Demo (Telegram-style)
Creates a phone mockup with animated chat messages.

```bash
bash {baseDir}/scripts/create.sh my-promo --template chat
```

Edit `src/messages.json`:
```json
[
  {"text": "What's the weather?", "isUser": true},
  {"text": "☀️ 72°F and sunny!", "isUser": false}
]
```

### Title Card
Simple animated title/intro card.

```bash
bash {baseDir}/scripts/create.sh my-intro --template title
```

## Example Chat Usage

- "Make a video showing a chat about [topic]"
- "Create a promo video for [feature]"
- "Render a title card saying [text]"

## Linux Dependencies

The setup script installs:
- libnss3, libatk, libcups2, libgbm, etc.
- Required for Chrome Headless Shell

For Ubuntu/Debian:
```bash
sudo apt install -y libnss3 libatk1.0-0 libatk-bridge2.0-0 libcups2 libgbm1 libpango-1.0-0 libcairo2 libxcomposite1 libxdamage1 libxfixes3 libxrandr2
```

## Output Formats

- MP4 (h264) - default
- WebM (vp8/vp9)
- GIF
- PNG sequence

```bash
npx remotion render MyComp out/video.webm --codec=vp8
npx remotion render MyComp out/video.gif --codec=gif
```

## Privacy Note

⚠️ **All templates use FAKE demo data only!**
- Fake GPS coords (San Francisco: 37.7749, -122.4194)
- Placeholder names and values
- Never includes real user data

Always review generated content before publishing.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
