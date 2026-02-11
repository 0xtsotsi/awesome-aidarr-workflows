# daily-motivation

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jhillin8/daily-motivation/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jhillin8/daily-motivation/SKILL.md)
> Category: AI & LLMs

---

## Description

Get daily motivation with personalized encouragement, goal reminders, and momentum tracking

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Get daily motivation with personalized encouragement, goal reminders, and momentum tracking

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run daily-motivation`)
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
You are executing the daily-motivation workflow. Use the following context:

Description: Get daily motivation with personalized encouragement, goal reminders, and momentum tracking

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: daily-motivation
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Daily Motivation

Fuel for your ambition. Get personalized encouragement, track progress, and stay accountable.

## What it does

- **Personalized motivation** - Tailored encouragement based on your goals and past wins
- **Goal reminders** - Contextual nudges that connect daily actions to bigger objectives
- **Win recalls** - Celebrate past achievements to build momentum
- **Momentum tracking** - Visual progress markers and streak counters

## Usage

**Get motivated**
- "motivate me" → receive personalized encouragement
- "inspire me" → get a powerful quote aligned to your goals

**Remind me why**
- "remind me of my goals" → see your top 3 active goals
- "why does this matter?" → context linking today's action to long-term vision

**Recall wins**
- "what have I accomplished?" → list recent wins and milestones
- "show me my streak" → view consistency tracking across habits

**Set intentions**
- "set today's intention" → frame the day around one key goal
- "what should I focus on?" → priority suggestion based on your goals

**Check momentum**
- "how's my progress?" → snapshot of current streaks, completions, trends
- "what's next?" → next actionable milestone

## Motivation Types

**Goal-based** - Anchor daily motivation to specific objectives you've set

**Quote-based** - Contextual, curated quotes matched to your current goals or mood

**Win-recall** - Pull from your achievement history to rebuild confidence

**Future visualization** - Paint a picture of what success looks like 30/90 days out

**Accountability** - Public or private commitment statements to strengthen resolve

## Tips

- Link motivation to real goals, not generic affirmations—specificity builds belief
- Use win-recalls before tackling hard tasks—momentum is real
- Set intentions daily, check momentum weekly—rhythm matters
- Connect daily micro-actions to 90-day outcomes—this makes motivation stick
- All data stays local on your machine

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
