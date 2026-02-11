# office-quotes

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/gumadeiras/office-quotes/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/gumadeiras/office-quotes/SKILL.md)
> Category: CLI Utilities

---

## Description

Generate random quotes from The Office (US). Provides access to 326 offline quotes plus online mode with SVG cards, character avatars, and full episode metadata via the akashrajpurohit API. Use for fun, icebreakers, or any task requiring The Office quotes.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate random quotes from The Office (US). Provides access to 326 offline quotes plus online mode with SVG cards, character avatars, and full episode metadata via the akashrajpurohit API. Use for fun, icebreakers, or any task requiring The Office quotes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run office-quotes`)
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
You are executing the office-quotes workflow. Use the following context:

Description: Generate random quotes from The Office (US). Provides access to 326 offline quotes plus online mode with SVG cards, character avatars, and full episode metadata via the akashrajpurohit API. Use for fun, icebreakers, or any task requiring The Office quotes.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: office-quotes
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# office-quotes Skill

Generate random quotes from The Office (US) TV show.

## Installation

```bash
npm install -g office-quotes-cli
```

## Usage

```bash
# Random offline quote (text only)
office-quotes

# API quote with SVG card
office-quotes --source api

# PNG output (best for Telegram)
office-quotes --source api --format png

# Light theme
office-quotes --source api --theme light
```

## Options

| Option | Description |
|--------|-------------|
| `--source <src>` | Quote source: local (default), api |
| `--format <fmt>` | Output format: svg, png, jpg, webp (default: svg) |
| `--theme <theme>` | SVG theme: dark, light (default: dark) |
| `--json` | Output as JSON |

## Quote Examples

> "Would I rather be feared or loved? Easy. Both. I want people to be afraid of how much they love me." — Michael Scott

> "Bears. Beets. Battlestar Galactica." — Jim Halpert

> "Whenever I'm about to do something, I think, 'Would an idiot do that?' And if they would, I do not do that thing." — Dwight Schrute

## Source

https://github.com/gumadeiras/office-quotes-cli

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
