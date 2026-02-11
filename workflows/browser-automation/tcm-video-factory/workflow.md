# tcm-video-factory

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xaotiensinh-abm/tcm-video-factory/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xaotiensinh-abm/tcm-video-factory/SKILL.md)
> Category: Browser & Automation

---

## Description

Automate health video production planning (Topic Research - Script - Character - Image/Video Prompts) using Perplexity API. Based on TCM Video Factory workflow.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Automate health video production planning (Topic Research - Script - Character - Image/Video Prompts) using Perplexity API. Based on TCM Video Factory workflow.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tcm-video-factory`)
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
You are executing the tcm-video-factory workflow. Use the following context:

Description: Automate health video production planning (Topic Research - Script - Character - Image/Video Prompts) using Perplexity API. Based on TCM Video Factory workflow.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tcm-video-factory
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# TCM Video Factory

Automated workflow to generate a complete video production plan including scripts, character design, and AI generation prompts (Nano Banana/VEO3).

## Usage

```bash
# Generate a plan for a specific topic
node skills/tcm-video-factory/index.mjs "Trà gừng mật ong"

# Generate a plan for a general theme (auto-research)
node skills/tcm-video-factory/index.mjs "Mẹo ngủ ngon"
```

## Output

Generates a `PLAN_[Timestamp].md` file in the current directory containing:
1.  Selected Topic
2.  Character Design Prompt (Pixar 3D)
3.  4-Part Script (32s total)
4.  Image Prompts (Start/End for each part)
5.  VEO3 Video Prompts (with Lip-sync)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
