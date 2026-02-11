# nano-triple

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/mvanhorn/nano-triple/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/mvanhorn/nano-triple/SKILL.md)
> Category: AI & LLMs

---

## Description

Generate 3 images with Nano Banana Pro using the same prompt. Pick the best, or give feedback on any option to get 3 refined versions.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate 3 images with Nano Banana Pro using the same prompt. Pick the best, or give feedback on any option to get 3 refined versions.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run nano-triple`)
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
You are executing the nano-triple workflow. Use the following context:

Description: Generate 3 images with Nano Banana Pro using the same prompt. Pick the best, or give feedback on any option to get 3 refined versions.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: nano-triple
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Nano Triple: 3 Images, Same Prompt, You Pick

When user wants an image, generate 3 versions and let them pick or refine.

## Flow

### Step 1: User Gives Their Prompt

User says: "make me an image of a sunset over mountains"

### Step 2: Generate 3 Images with THE SAME PROMPT

Use the user's EXACT prompt for all 3. Don't modify it, don't get creative. The model's inherent randomness will produce 3 different results.

Run all 3 in parallel:

```bash
# Same prompt, 3 times
uv run ~/.npm-global/lib/node_modules/clawdbot/skills/nano-banana-pro/scripts/generate_image.py \
  --prompt "[USER'S EXACT PROMPT]" \
  --filename "option-1.png" --resolution 1K

uv run ~/.npm-global/lib/node_modules/clawdbot/skills/nano-banana-pro/scripts/generate_image.py \
  --prompt "[USER'S EXACT PROMPT]" \
  --filename "option-2.png" --resolution 1K

uv run ~/.npm-global/lib/node_modules/clawdbot/skills/nano-banana-pro/scripts/generate_image.py \
  --prompt "[USER'S EXACT PROMPT]" \
  --filename "option-3.png" --resolution 1K
```

### Step 3: Send All 3 Images Labeled 1, 2, 3

Send each image with just the number:

- **1** [image]
- **2** [image]
- **3** [image]

**NO descriptions. NO creativity. Just 1, 2, 3 and the images.**

### Step 4: User Picks or Gives Feedback

- "2" → Done, that's the winner
- "1 but warmer colors" → Generate 3 MORE with their feedback applied
- "none, try again" → Generate 3 more with same prompt

**Key: Feedback on any option = 3 new images with that feedback applied**

## Example

**User:** make me an image of a cat wearing a top hat

**You:** Generate 3 images using that exact prompt, send as 1, 2, 3

**User:** 2 but bigger hat

**You:** Generate 3 MORE images with "bigger hat" added to prompt, send as 1, 2, 3

**User:** 3

**You:** 👍

## Rules

1. **Always 3 images** - Same prompt, 3 outputs
2. **No creativity** - Use user's exact prompt
3. **Label 1, 2, 3** - No descriptions
4. **Feedback = 3 more** - Any edit request generates 3 new options

## API Key

Uses `GEMINI_API_KEY` from environment or clawdbot config.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
