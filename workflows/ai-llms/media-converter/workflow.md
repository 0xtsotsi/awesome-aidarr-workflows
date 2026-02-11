# media-converter

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/autogame-17/media-converter/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/autogame-17/media-converter/SKILL.md)
> Category: AI & LLMs

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
**Trigger:** User-invocable (via `aidarr run media-converter`)
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
You are executing the media-converter workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: media-converter
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Media Converter Skill

## Description
Detects media file types via magic bytes and fixes file extensions to ensure compatibility with Gemini (which rejects `application/octet-stream`). Handles basic conversion logic (placeholder for future ffmpeg support).

## Usage
```bash
# Detect MIME type and return JSON
node skills/media-converter/index.js detect --file <path>

# Fix extension based on detected MIME (renames file if needed)
node skills/media-converter/index.js fix --file <path>
```

## Examples
```bash
# Check a file masked as .bin
node skills/media-converter/index.js detect --file /tmp/unknown.bin
# Output: {"mime": "image/gif", "ext": "gif"}

# Rename a file to match its content
node skills/media-converter/index.js fix --file /tmp/unknown.bin
# Output: {"original": "/tmp/unknown.bin", "fixed": "/tmp/unknown.gif", "mime": "image/gif"}
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
