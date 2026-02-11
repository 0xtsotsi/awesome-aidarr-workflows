# weekly-synthesis

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/itsflow/weekly-synthesis/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/itsflow/weekly-synthesis/SKILL.md)
> Category: Personal Development

---

## Description

Create a comprehensive synthesis of the week's work and thinking

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** productivity, review, synthesis, patterns

---

## GOTCHA Framework

### G - Goals
Create a comprehensive synthesis of the week's work and thinking

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run weekly-synthesis`)
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
You are executing the weekly-synthesis workflow. Use the following context:

Description: Create a comprehensive synthesis of the week's work and thinking

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: weekly-synthesis
category: Personal Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Weekly Synthesis

Create a comprehensive synthesis of the week's work and thinking.

## Usage

```
/weekly-synthesis
```

## Analysis Process

1. **Gather Week's Work**
   - All notes created this week
   - All notes modified this week
   - Projects that saw activity

2. **Identify Patterns**
   - Recurring themes
   - Common challenges
   - Breakthrough moments
   - Energy patterns (what energized vs drained)

3. **Synthesize Learning**
   - Key insights that emerged
   - How thinking evolved
   - Connections discovered
   - Questions answered and raised

4. **Assess Progress**
   - Projects advanced
   - Areas maintained
   - Resources added
   - Items archived

## Output Format

Create a weekly synthesis note:

```markdown
# Weekly Synthesis - Week of [Date]

## Week at a Glance

- Notes created: [X]
- Projects active: [List]
- Major accomplishments: [List]

## Key Themes

### Theme 1: [Name]

- Where it appeared: [contexts]
- Why it matters: [significance]
- Next actions: [what to do]

### Theme 2: [Name]

- Where it appeared: [contexts]
- Why it matters: [significance]
- Next actions: [what to do]

## Major Insights

1. [Insight with context]
2. [Insight with context]

## Progress by Project

### [Project Name]

- What advanced:
- What's blocked:
- Next week's focus:

## Questions Emerged

- [Question 1 - and why it matters]
- [Question 2 - and why it matters]

## Energy Audit

- What gave energy:
- What drained energy:
- What to adjust:

## Connections Made

- [Note A] <-> [Note B]: [Why significant]
- [Concept X] <-> [Concept Y]: [New understanding]

## Next Week's Intentions

1. [Primary focus]
2. [Secondary focus]
3. [Thing to explore]

## To Process

- Inbox items: [count]
- Orphaned notes: [list]
- Missing connections: [identified]
```

## Follow-up Actions

- Archive completed projects
- Clean up inbox
- Update project status
- Plan next week's focus

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
