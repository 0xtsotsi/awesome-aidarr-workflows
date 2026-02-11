# tesy

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kipasdinding6969-alt/tesy/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kipasdinding6969-alt/tesy/SKILL.md)
> Category: Productivity & Tasks

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
**Trigger:** User-invocable (via `aidarr run tesy`)
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
You are executing the tesy workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tesy
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

> Related: [[AGENTS]], [[skills/pai-redteam/Workflows/AdversarialValidation|AdversarialValidation]], [[skills/pai-redteam/Integration|Integration]]

---
name: RedTeam
description: Adversarial analysis with 32 agents. USE WHEN red team, attack idea, counterarguments, critique, stress test. SkillSearch('redteam') for docs.
---

## Customization

**Before executing, check for user customizations at:**
`~/.claude/skills/CORE/USER/SKILLCUSTOMIZATIONS/RedTeam/`

If this directory exists, load and apply any PREFERENCES.md, configurations, or resources found there. These override default behavior. If the directory does not exist, proceed with skill defaults.

# RedTeam Skill

Military-grade adversarial analysis using parallel agent deployment. Breaks arguments into atomic components, attacks from 32 expert perspectives (engineers, architects, pentesters, interns), synthesizes findings, and produces devastating counter-arguments with steelman representations.


## Voice Notification

**When executing a workflow, do BOTH:**

1. **Send voice notification**:
   ```bash
   curl -s -X POST http://localhost:8888/notify \
     -H "Content-Type: application/json" \
     -d '{"message": "Running the WORKFLOWNAME workflow from the RedTeam skill"}' \
     > /dev/null 2>&1 &
   ```

2. **Output text notification**:
   ```
   Running the **WorkflowName** workflow from the **RedTeam** skill...
   ```

**Full documentation:** `~/.claude/skills/CORE/SkillNotifications.md`

## Workflow Routing

Route to the appropriate workflow based on the request.

**When executing a workflow, output this notification directly:**

```
Running the **WorkflowName** workflow from the **RedTeam** skill...
```

| Trigger | Workflow |
|---------|----------|
| Red team analysis (stress-test existing content) | `Workflows/ParallelAnalysis.md` |
| Adversarial validation (produce new content via competition) | `Workflows/AdversarialValidation.md` |

---

## Quick Reference

| Workflow | Purpose | Output |
|----------|---------|--------|
| **ParallelAnalysis** | Stress-test existing content | Steelman + Counter-argument (8-points each) |
| **AdversarialValidation** | Produce new content via competition | Synthesized solution from competing proposals |

**The Five-Phase Protocol (ParallelAnalysis):**
1. **Decomposition** - Break into 24 atomic claims
2. **Parallel Analysis** - 32 agents examine strengths AND weaknesses
3. **Synthesis** - Identify convergent insights
4. **Steelman** - Strongest version of the argument
5. **Counter-Argument** - Strongest rebuttal

---

## Context Files

- `Philosophy.md` - Core philosophy, success criteria, agent types
- `Integration.md` - Skill integration, FirstPrinciples usage, output format

---

## Examples

**Attack an architecture proposal:**
```
User: "red team this microservices migration plan"
--> Workflows/ParallelAnalysis.md
--> Returns steelman + devastating counter-argument (8 points each)
```

**Devil's advocate on a business decision:**
```
User: "poke holes in my plan to raise prices 20%"
--> Workflows/ParallelAnalysis.md
--> Surfaces the ONE core issue that could collapse the plan
```

**Adversarial validation for content:**
```
User: "battle of bots - which approach is better for this feature?"
--> Workflows/AdversarialValidation.md
--> Synthesizes best solution from competing ideas
```

---

**Last Updated:** 2025-12-20

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
