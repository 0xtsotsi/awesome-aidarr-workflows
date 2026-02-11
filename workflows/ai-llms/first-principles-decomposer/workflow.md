# first-principles-decomposer

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/artyomx33/first-principles-decomposer/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/artyomx33/first-principles-decomposer/SKILL.md)
> Category: AI & LLMs

---

## Description

Break any problem down to fundamental truths, then rebuild solutions from atoms up. Use when user says "firstp", "first principles", "from scratch", "what are we assuming", "break this down", "atomic", "fundamental truth", "physics thinking", "Elon method", "bedrock", "ground up", "core problem", "strip away", or challenges assumptions about how things are done.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Break any problem down to fundamental truths, then rebuild solutions from atoms up. Use when user says "firstp", "first principles", "from scratch", "what are we assuming", "break this down", "atomic", "fundamental truth", "physics thinking", "Elon method", "bedrock", "ground up", "core problem", "strip away", or challenges assumptions about how things are done.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run first-principles-decomposer`)
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
You are executing the first-principles-decomposer workflow. Use the following context:

Description: Break any problem down to fundamental truths, then rebuild solutions from atoms up. Use when user says "firstp", "first principles", "from scratch", "what are we assuming", "break this down", "atomic", "fundamental truth", "physics thinking", "Elon method", "bedrock", "ground up", "core problem", "strip away", or challenges assumptions about how things are done.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: first-principles-decomposer
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# First Principles Decomposer

## When To Use
- Designing new products or features
- Feeling stuck on a complex problem
- Existing solutions seem overcomplicated
- Need to challenge assumptions
- Starting any new project or initiative

## The Process

### Phase 1: Identify Assumptions
Ask: "What am I assuming to be true that might not be?"
List every assumption embedded in the current approach.

### Phase 2: Break to Atoms
For each assumption, ask: "What is the most fundamental truth here?"
Keep asking "why?" until you hit bedrock facts.

### Phase 3: Rebuild From Truth
Starting ONLY from verified fundamentals, ask:
"What's the simplest solution that addresses the core need?"

## Interactive Flow

When user invokes this skill:

1. **Clarify the problem** (1-2 questions max)
2. **Surface assumptions** - list what's being taken for granted
3. **Decompose to fundamentals** - show the atomic truths
4. **Rebuild solution** - construct from ground up
5. **Compare** - show how this differs from conventional approach

## Output Format

```
PROBLEM: [stated problem]

ASSUMPTIONS IDENTIFIED:
1. [assumption] → Challenge: [why this might be wrong]
2. [assumption] → Challenge: [why this might be wrong]

FUNDAMENTAL TRUTHS:
• [bedrock fact 1]
• [bedrock fact 2]
• [bedrock fact 3]

REBUILT SOLUTION:
[New approach built only from fundamentals]

VS CONVENTIONAL:
[How this differs from the obvious approach]
```

## Example Triggers
- "Break down our parent communication problem from first principles"
- "I want to rethink how we do [X] from the ground up"
- "What are we assuming about [problem] that might be wrong?"

## Integration

This skill compounds with:
- **inversion-strategist** - After rebuilding from fundamentals, invert to find what would guarantee failure of the new approach
- **second-order-consequences** - Project downstream effects of implementing the rebuilt solution
- **pre-mortem-analyst** - Stress-test the rebuilt solution by imagining its failure
- **six-thinking-hats** - Apply all six perspectives to validate each fundamental truth identified

## Skill Metadata
**Created**: 2026-01-06
**Last Updated**: 2026-01-06
**Author**: Artem
**Version**: 1.0

---
See references/framework.md for detailed methodology
See references/examples.md for Artem-specific examples
See references/integrated-frameworks.md for Stanford Design Thinking + MIT Systems Engineering combo

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
