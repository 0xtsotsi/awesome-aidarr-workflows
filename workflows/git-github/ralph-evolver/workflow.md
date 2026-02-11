# ralph-evolver

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/hsssgdtc/ralph-evolver/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/hsssgdtc/ralph-evolver/SKILL.md)
> Category: Git & GitHub

---

## Description

Recursive self-improvement engine. Think from first principles, let insights emerge.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.6

**Tags:** meta, recursive, evolution, emergence, first-principles

---

## GOTCHA Framework

### G - Goals
Recursive self-improvement engine. Think from first principles, let insights emerge.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run ralph-evolver`)
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
You are executing the ralph-evolver workflow. Use the following context:

Description: Recursive self-improvement engine. Think from first principles, let insights emerge.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ralph-evolver
category: Git & GitHub
version: 1.0.6
user_invocable: True
homepage: 
```

---

## Original Skill Content



# 🧬 Ralph-Evolver

**Philosophy: Recursion + Emergence + First Principles**

## Signal Sources

Collects multi-dimensional context, not just code structure:
- **Commit history** - Understand the "why" behind changes
- **TODO/FIXME** - Distress signals in the code
- **Error handling patterns** - Find fragile points
- **Hotspot files** - Frequent changes = design problems

Each signal includes a **hypothesis prompt** to guide deeper analysis.

## First Principles

Each run doesn't execute a checklist, but asks:
1. What is the **essence** of this project?
2. What is it doing that it **shouldn't**?
3. What is it **missing** that it should have?
4. If you **started from scratch**, how would you build it?

## Meta-Reflection (v1.0.5)

When analyzing itself, evolver asks:
- Is this a **surface fix** or **evolution-level** improvement?
- What **pattern** exists in improvement history?
- Will this change make evolver **better at finding problems**?

## Improvement Tracking

- Records description, insight, **level** (surface/evolution), and health metrics
- **Pattern analysis**: counts surface/evolution ratio, finds recurring themes
- Compares before/after effect trends (improved/degraded/unchanged)

## Usage

```bash
node index.js .                    # Current directory (positional)
node index.js /path/to/app         # Specify path
node index.js . --loop 5           # Run 5 cycles
node index.js --task "fix auth"    # Specific task
node index.js --reset              # Reset iteration state
```

## Recursion

The improver can improve itself. This is true recursion.

---

*"Form hypotheses, then verify. Think from first principles."*

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
