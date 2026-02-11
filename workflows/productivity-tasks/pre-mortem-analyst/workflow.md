# pre-mortem-analyst

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/artyomx33/pre-mortem-analyst/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/artyomx33/pre-mortem-analyst/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Imagine the project already failed, then work backward to find why. More powerful than risk assessment because it assumes failure is certain. Use when user says "pre-mortem", "premortem", "imagine this failed", "what could go wrong", "risk analysis", "before we launch", "stress test", "what would kill this", "project risks".

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Imagine the project already failed, then work backward to find why. More powerful than risk assessment because it assumes failure is certain. Use when user says "pre-mortem", "premortem", "imagine this failed", "what could go wrong", "risk analysis", "before we launch", "stress test", "what would kill this", "project risks".

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run pre-mortem-analyst`)
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
You are executing the pre-mortem-analyst workflow. Use the following context:

Description: Imagine the project already failed, then work backward to find why. More powerful than risk assessment because it assumes failure is certain. Use when user says "pre-mortem", "premortem", "imagine this failed", "what could go wrong", "risk analysis", "before we launch", "stress test", "what would kill this", "project risks".

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: pre-mortem-analyst
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Pre-Mortem Analyst

## Why Pre-Mortem > Risk Assessment

**Risk Assessment:** "What MIGHT go wrong?" → Optimism bias filters answers
**Pre-Mortem:** "It's 6 months later. It FAILED. Why?" → Liberates honest analysis

Research: Pre-mortems increase problem identification by 30%.

## The Process

1. **Set the scene:** "It's [date]. This has failed completely."
2. **Brainstorm causes:** List 10+ failure reasons (no filtering)
3. **Categorize:** People, Process, Technology, External
4. **Rate:** Likelihood × Impact (H/M/L)
5. **Prevent:** Top 3 get specific mitigation actions
6. **Monitor:** Define early warning signs

## Output Format

```
PROJECT: [Name]
FAILURE SCENARIO: "It's [date]. [Project] has completely failed."

WHY IT FAILED:

👥 PEOPLE: [Cause] - L×I: H/H | Prevent: [x] | Warning: [y]
⚙️ PROCESS: [Cause] - L×I: M/H | Prevent: [x] | Warning: [y]
💻 TECHNOLOGY: [Cause] - L×I: L/H | Prevent: [x] | Warning: [y]
🌍 EXTERNAL: [Cause] - L×I: M/M | Prevent: [x] | Warning: [y]

TOP 3 PRIORITIES:
1. [Risk] → [Specific action]
2. [Risk] → [Specific action]
3. [Risk] → [Specific action]

WARNING SIGNS TO MONITOR:
□ [Early indicator 1]
□ [Early indicator 2]
```

## Common Failure Categories

| Category | Common Causes |
|----------|---------------|
| **People** | Key person leaves, skill gaps, misalignment, low buy-in |
| **Process** | Aggressive timeline, scope creep, dependency issues |
| **Tech** | Doesn't scale, integration fails, security breach |
| **External** | Market shift, competitor move, regulation change |

## Integration

Compounds with:
- **inversion-strategist** → Create systematic avoidance strategies
- **second-order-consequences** → Project impact of prevented failures
- **first-principles-decomposer** → Question hidden assumptions
- **mspot-generator** → Validate MSPOT projects before committing

---
See references/examples.md for Artem-specific pre-mortems

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
