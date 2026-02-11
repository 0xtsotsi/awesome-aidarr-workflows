# vestaboard

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/seidprojects/vestaboard/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/seidprojects/vestaboard/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Read and write messages on a Vestaboard using the Vestaboard Cloud API (cloud.vestaboard.com) and optional legacy RW endpoint. Use when asked to display text on a Vestaboard, update a sign/board, show a short status message, render simple pixel-art using color/filled character codes, or retrieve the current board message.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Read and write messages on a Vestaboard using the Vestaboard Cloud API (cloud.vestaboard.com) and optional legacy RW endpoint. Use when asked to display text on a Vestaboard, update a sign/board, show a short status message, render simple pixel-art using color/filled character codes, or retrieve the current board message.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run vestaboard`)
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
You are executing the vestaboard workflow. Use the following context:

Description: Read and write messages on a Vestaboard using the Vestaboard Cloud API (cloud.vestaboard.com) and optional legacy RW endpoint. Use when asked to display text on a Vestaboard, update a sign/board, show a short status message, render simple pixel-art using color/filled character codes, or retrieve the current board message.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: vestaboard
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Vestaboard

## Security
- Require a token via environment variables (never inline keys in prompts, logs, or commits).
  - Preferred: `VESTABOARD_TOKEN`
  - Optional legacy fallback: `VESTABOARD_RW_KEY`

## Constraints
- Flagship Vestaboard layout is **6 rows x 22 cols**.
- Text input is formatted to 6x22 by default (uppercase + word wrap; truncates overflow).

## Quick usage (local CLI)

```bash
# from repo root
npm install

# Preview formatting only
node scripts/vb.js preview "Hello from Quarterbridge Farm"

# Read current message (JSON)
node scripts/vb.js read

# Write text
node scripts/vb.js write "EGGS READY"

# Write a numeric layout (6x22 array of character codes)
node scripts/vb.js write-layout content/layouts/forest-depth.json
```

## Sample content
- Numeric layouts live in `content/layouts/*.json`
- Human review previews live in `content/previews/*.md`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
