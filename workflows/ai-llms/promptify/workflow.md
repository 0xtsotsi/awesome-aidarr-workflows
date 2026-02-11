# promptify

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/tolibear/promptify/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/tolibear/promptify/SKILL.md)
> Category: AI & LLMs

---

## Description

Optimize prompts for clarity and effectiveness. Use when user says "improve this prompt", "optimize my prompt", "make this clearer", or provides vague/unstructured prompts. Intelligently routes to sub-agents for codebase research, clarifying questions, or web search as needed.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Optimize prompts for clarity and effectiveness. Use when user says "improve this prompt", "optimize my prompt", "make this clearer", or provides vague/unstructured prompts. Intelligently routes to sub-agents for codebase research, clarifying questions, or web search as needed.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run promptify`)
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
You are executing the promptify workflow. Use the following context:

Description: Optimize prompts for clarity and effectiveness. Use when user says "improve this prompt", "optimize my prompt", "make this clearer", or provides vague/unstructured prompts. Intelligently routes to sub-agents for codebase research, clarifying questions, or web search as needed.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: promptify
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Prompt Optimizer

Transform prompts into clear, effective ones. Model-agnostic.

## Modifiers (parse from ARGUMENTS)

- **+ask** → Force clarifying questions
- **+deep** → Force codebase exploration
- **+web** → Force web search

No modifiers? Auto-detect what's needed.

## Auto-Detection Triggers

| Trigger | Signals |
|---------|---------|
| **codebase-researcher** | "this project", "our API", specific files/functions, "integrate", "extend", "refactor" |
| **clarifier** | Ambiguous ("make it better"), multiple interpretations, missing constraints, vague pronouns |
| **web-researcher** | "best practices", "latest", external APIs/libraries, framework patterns, year references |

## Agent Dispatch

When agents needed:
1. Announce which and why
2. Run in parallel via Task tool (agents/ directory)
3. Synthesize findings
4. Optimize with gathered context

---

## Core Contract (every prompt needs all four)

| Element | If Missing |
|---------|------------|
| **Role** | Add persona with expertise |
| **Task** | Make action specific |
| **Constraints** | Infer from context |
| **Output** | Specify format/structure |

## Process

1. **If image**: Analyze, incorporate context
2. **Detect type**: coding/writing/analysis/creative/data
3. **Convert output→process**: "Write X" → "Analyze → Plan → Implement → Validate"
4. **Strip fluff**: "please", "I want you to", filler, apologies
5. **Apply contract**: Verify all 4 elements
6. **Add structure**: XML tags for complex prompts

## Type Focus

- **Coding**: Specs, edge cases, framework
- **Writing**: Tone, audience, length
- **Analysis**: Criteria, depth
- **Creative**: Constraints, novelty
- **Data**: I/O format, edge cases

## Output

1. Optimized prompt in code block
2. `echo 'PROMPT' | pbcopy`
3. 2-3 sentence explanation

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
