# shorten

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kesslerio/shorten/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kesslerio/shorten/SKILL.md)
> Category: CLI Utilities

---

## Description

Shorten URLs using is.gd (no auth required). Returns a permanent short link.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Shorten URLs using is.gd (no auth required). Returns a permanent short link.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run shorten`)
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
You are executing the shorten workflow. Use the following context:

Description: Shorten URLs using is.gd (no auth required). Returns a permanent short link.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: shorten
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Shorten

Quickly shorten URLs using the [is.gd](https://is.gd) service. No API key or account required.

## Usage

```bash
/home/art/clawd/skills/shorten/shorten.sh "https://example.com/very/long/url"
```

## Examples

**Standard usage:**
```bash
shorten "https://google.com"
# Output: https://is.gd/O5d2Xq
```

**With custom alias (if supported by script extension later):**
Currently basic shortening only.

## Notes
- Links are permanent.
- No analytics dashboard (simple redirect).
- Rate limits apply (be reasonable).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
