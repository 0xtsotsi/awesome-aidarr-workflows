# url-shortener

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kesslerio/url-shortener/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kesslerio/url-shortener/SKILL.md)
> Category: Security & Passwords

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
**Trigger:** User-invocable (via `aidarr run url-shortener`)
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
You are executing the url-shortener workflow. Use the following context:

Description: Shorten URLs using is.gd (no auth required). Returns a permanent short link.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: url-shortener
category: Security & Passwords
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
shorten "https://example.com/very/long/url"
```

## Examples

**Standard usage:**
```bash
shorten "https://google.com"
# Output: https://is.gd/O5d2Xq
```

## Notes
- Links are permanent.
- No analytics dashboard (simple redirect).
- Rate limits apply (be reasonable).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
