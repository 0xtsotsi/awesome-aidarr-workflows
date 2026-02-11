# trmnl-display

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/peetzweg/trmnl-display/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/peetzweg/trmnl-display/SKILL.md)
> Category: CLI Utilities

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
**Trigger:** User-invocable (via `aidarr run trmnl-display`)
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
You are executing the trmnl-display workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: trmnl-display
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# TRMNL Display Skill

This skill sends content to a TRMNL e-ink display device using the webhook API.

## Webhook Configuration

- **Endpoint:** `https://trmnl.com/api/custom_plugins/0d9e7125-789d-46a6-9a51-070ac95364d8`
- **Method:** POST
- **Content-Type:** application/json

## How to Send a Message

Use curl to POST a JSON payload with `merge_variables`:

```bash
curl "https://trmnl.com/api/custom_plugins/0d9e7125-789d-46a6-9a51-070ac95364d8" \
  -H "Content-Type: application/json" \
  -d '{"merge_variables": {"title": "Your Title Here", "text": "Your message content here"}}' \
  -X POST
```

## Available Merge Variables

The TRMNL device is configured with a template that supports these variables:

| Variable | Description |
|----------|-------------|
| `title` | The main heading displayed prominently |
| `text` | The body content below the title (supports Markdown) |
| `image` | Fully qualified URL to an image (displayed on the right side) |

## Markdown Support

The `text` field supports Markdown formatting for richer content:

- **Bold:** `**text**`
- **Italic:** `*text*`
- **Lists:** Use `- item` or `1. item`
- **Line breaks:** Use `\n` in the JSON string
- **Headers:** `## Heading` (use sparingly, title is already prominent)

## Usage Examples

**Simple notification:**
```json
{"merge_variables": {"title": "Reminder", "text": "Stand up and stretch!"}}
```

**Status update with formatting:**
```json
{"merge_variables": {"title": "Build Status", "text": "**All tests passing**\n\nReady to deploy."}}
```

**List format:**
```json
{"merge_variables": {"title": "Today's Tasks", "text": "- Review PR #42\n- Update docs\n- Team standup at 10am"}}
```

**Weather-style info:**
```json
{"merge_variables": {"title": "San Francisco", "text": "**Sunny, 72°F**\n\nPerfect day for a walk"}}
```

**With image:**
```json
{"merge_variables": {"title": "Album of the Day", "text": "**Kind of Blue**\nMiles Davis", "image": "https://example.com/album-cover.jpg"}}

## Instructions for Claude

When the user asks to send something to their TRMNL device:

1. Parse the user's request to extract a title and message
2. If only a message is provided, generate an appropriate short title
3. Keep titles concise (under 30 characters recommended)
4. Keep text brief - e-ink displays work best with short, readable content
5. Use Markdown formatting to enhance readability (bold for emphasis, lists for multiple items)
6. If relevant, include an image URL (must be a fully qualified public URL)
7. Send the webhook using the curl command above
8. Confirm to the user what was sent

If the user provides arguments like `/trmnl Meeting in 5 minutes`, interpret the first few words as a potential title and the rest as the message, or use your judgment to create an appropriate title/text split.

## Response Handling

A successful response looks like:
```json
{"message":null,"merge_variables":{"title":"...","text":"..."}}
```

If you see an error message in the response, inform the user of the issue.

## Notes

- The device refreshes periodically, so content may not appear instantly
- E-ink displays are monochrome - no color support
- Keep content concise for best readability on the small screen
- Images must be fully qualified public URLs (e.g., `https://example.com/image.png`)
- Images are displayed on the right side in a two-column layout

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
