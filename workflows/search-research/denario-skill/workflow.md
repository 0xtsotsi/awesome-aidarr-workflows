# denario-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jmanhype/denario-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jmanhype/denario-skill/SKILL.md)
> Category: Search & Research

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
**Trigger:** User-invocable (via `aidarr run denario-skill`)
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
You are executing the denario-skill workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: denario-skill
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Denario Skill

Wraps the **Denario** framework to automate the scientific research process. Handles environment setup and Z.ai integration automatically.

**Engine:** `scripts/wrapper.sh`
**Working Directory:** `./` (Skill Root)

---

## Trigger Phrases

| Phrase | Action |
|--------|--------|
| **"Denario idea"** | Generate research ideas (Maker/Hater loop). |
| **"Denario methods"** | Develop methodology. |
| **"Denario results"** | Generate results and analysis. |
| **"Denario paper"** | Compile full paper. |
| **"Denario citations"** | Manage citations. |

---

## Usage Guide

### 1. Generating an Idea
> **User:** "Denario idea"
> **Bot:** Runs the wrapper script to execute `test_denario.py`. First run will auto-install dependencies.

### 2. Full Pipeline
> **User:** "Denario methods", then "Denario results", then "Denario paper"
> **Bot:** Progresses through the research stages.

---

## Configuration

**API Key Required:**
You must set your Z.ai/Zhipu API key in Clawdbot's environment:
```bash
clawdbot config set env.OPENAI_API_KEY <your-key>
```

**Environment:**
Creates and manages a virtualenv at `~/.denario_skill_env` automatically.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
