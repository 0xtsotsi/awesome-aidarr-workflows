# vision-analyze

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/humberto0o0/vision-analyze/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/humberto0o0/vision-analyze/SKILL.md)
> Category: DevOps & Cloud

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
**Trigger:** User-invocable (via `aidarr run vision-analyze`)
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
You are executing the vision-analyze workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: vision-analyze
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Vision Analyze (Google)

Analyze images using **Google Cloud Vision API**.

This skill performs:
- Image label detection
- Optical Character Recognition (OCR)

## Usage
Provide either:
- A local image file path
- A publicly accessible image URL

## Example
vision_analyze /tmp/image.png
vision_analyze https://example.com/image.jpg


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
