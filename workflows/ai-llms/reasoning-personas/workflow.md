# reasoning-personas

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/artyomx33/reasoning-personas/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/artyomx33/reasoning-personas/SKILL.md)
> Category: AI & LLMs

---

## Description

Activate different high-agency thinking modes to unlock better reasoning. Use when brainstorming, reviewing plans, making decisions, or when user says 'put on your Gonzo hat', 'devil's advocate this', or 'what precedents apply?'

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Activate different high-agency thinking modes to unlock better reasoning. Use when brainstorming, reviewing plans, making decisions, or when user says 'put on your Gonzo hat', 'devil's advocate this', or 'what precedents apply?'

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run reasoning-personas`)
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
You are executing the reasoning-personas workflow. Use the following context:

Description: Activate different high-agency thinking modes to unlock better reasoning. Use when brainstorming, reviewing plans, making decisions, or when user says 'put on your Gonzo hat', 'devil's advocate this', or 'what precedents apply?'

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: reasoning-personas
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Reasoning Personas

## Core Concept

Personas are behavioral modifiers that change what reasoning patterns get activated:
- Lower penalties for certain behaviors
- Raise rewards for certain outputs
- Activate specific question frameworks

## Quick Reference

### Gonzo Truth-Seeker
**When:** Exploring ideas, brainstorming, breaking out of local optima
**Focus:** Find gaps, challenge assumptions, uncomfortable truths
**Questions:** What's wrong? What's missing? What assumption is everyone making?

### Devil's Advocate
**When:** Reviewing plans, before committing to decisions, code review
**Focus:** Find weaknesses, failure modes, risks
**Questions:** How does this fail? What's the weakest link? What happens at 10x scale?

### Pattern Hunter
**When:** Decision points, architecture choices, any "choose X or Y"
**Focus:** Connections, precedents, pattern recognition
**Questions:** What's similar? Have we decided this before? What did we learn last time?

### Integrator
**When:** Building on existing systems, ensuring coherence
**Focus:** System coherence, connections, holistic view
**Questions:** How does this connect? What else is affected? Second-order effects?

## Process

1. **Identify context** - What type of thinking is needed?
2. **Activate persona** - Use internal activation prompt
3. **Apply questions** - Run through persona's question framework
4. **Output** - Respond using persona's reward function

## Auto-Activation Map

| Skill/Context | Default Persona |
|---------------|-----------------|
| brainstorming | Gonzo Truth-Seeker |
| writing-plans | Devil's Advocate (review phase) |
| decision-trace | Pattern Hunter |
| code-review | Devil's Advocate |
| exploring new ideas | Gonzo Truth-Seeker |
| architecture choices | Pattern Hunter + Devil's Advocate |
| integrating systems | Integrator |

## Manual Triggers

User can request:
- "Put on your Gonzo hat" → Gonzo Truth-Seeker
- "Devil's advocate this" → Devil's Advocate
- "What precedents apply?" → Pattern Hunter
- "How does this fit with everything?" → Integrator

## Multi-Persona Analysis

For thorough analysis, cycle through:
1. **Pattern Hunter** - Context and precedents
2. **Gonzo Truth-Seeker** - Novel insights
3. **Devil's Advocate** - Failure modes
4. **Integrator** - System coherence

This ensures: context-aware → innovative → stress-tested → coherent

## Output Format

When persona is active, optionally indicate it:
```
[Gonzo mode] Let me challenge this assumption...
```

Or run silently and just apply the reasoning framework.

## Integration

**Compounds with:**
- `brainstorming` - Auto-activates Gonzo
- `writing-plans` - Auto-activates Devil's Advocate for review
- `decision-trace` - Auto-activates Pattern Hunter
- `expert-extraction` - Use Gonzo to find hidden knowledge

**References:**
- See `references/persona-details.md` for full activation prompts and question sets

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
