# frinkiac

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ryantenney/frinkiac/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ryantenney/frinkiac/SKILL.md)
> Category: Browser & Automation

---

## Description

Search TV show screenshots and generate memes from The Simpsons, Futurama, Rick and Morty, and 30 Rock

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search TV show screenshots and generate memes from The Simpsons, Futurama, Rick and Morty, and 30 Rock

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run frinkiac`)
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
You are executing the frinkiac workflow. Use the following context:

Description: Search TV show screenshots and generate memes from The Simpsons, Futurama, Rick and Morty, and 30 Rock

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: frinkiac
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Frinkiac TV Screenshot & Meme Tool

Search dialogue, browse scenes, and generate memes from popular TV shows using the Frinkiac/Morbotron APIs.

## Available Shows

- `simpsons` - The Simpsons (via Frinkiac)
- `futurama` - Futurama (via Morbotron)
- `rickandmorty` - Rick and Morty
- `30rock` - 30 Rock

## MCP Server Setup

This skill uses an MCP server. Add to your MCP config:

```json
{
  "mcpServers": {
    "frinkiac": {
      "command": "npx",
      "args": ["-y", "@ryantenney/frinkiac-mcp"]
    }
  }
}
```

## Tools

### search

Search for scenes by dialogue text.

- `show`: Which show to search (simpsons, futurama, rickandmorty, 30rock)
- `query`: Dialogue to search for (e.g., "D'oh!", "Good news everyone")
- `limit`: Max results (optional)
- `include_images`: Include thumbnails (optional)

### get_caption

Get detailed scene info including episode metadata and nearby frames.

- `show`: Which show
- `episode`: Episode key in S##E## format (e.g., "S07E21")
- `timestamp`: Frame timestamp in milliseconds
- `include_nearby_images`: Include thumbnails for nearby frames (optional)

### get_screenshot

Get a screenshot image from a specific scene.

- `show`: Which show
- `episode`: Episode key in S##E## format
- `timestamp`: Frame timestamp in milliseconds
- `return_url_only`: Return URL instead of image data (optional)

### generate_meme

Create a meme with custom text overlay. Text auto-wraps at ~35 characters per line.

- `show`: Which show
- `episode`: Episode key in S##E## format
- `timestamp`: Frame timestamp in milliseconds
- `text`: Text to overlay on the image

### get_nearby_frames

Browse adjacent frames to find the perfect screenshot.

- `show`: Which show
- `episode`: Episode key in S##E## format
- `timestamp`: Frame timestamp in milliseconds
- `include_images`: Include thumbnails (optional)

### get_episode

Get episode metadata and subtitles within a timestamp range.

- `show`: Which show
- `episode`: Episode key in S##E## format
- `start_timestamp`: Start of range in milliseconds
- `end_timestamp`: End of range in milliseconds

## Example Workflows

**Find and meme a quote:**

1. Search for dialogue: `search simpsons "everything's coming up Milhouse"`
2. Get the screenshot: `get_screenshot` with episode/timestamp from results
3. Generate meme: `generate_meme` with custom text

**Browse a scene:**

1. Search for a quote to get episode/timestamp
2. Use `get_nearby_frames` to find the perfect frame
3. Use `get_caption` to see full context and subtitles

**Get episode context:**

1. Use `get_episode` with a timestamp range to see all dialogue in a scene
2. Find the exact moment you want
3. Generate a meme or screenshot

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
