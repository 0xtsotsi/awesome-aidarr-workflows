# habit-tracker

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jhillin8/habit-tracker/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jhillin8/habit-tracker/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Build habits with streaks, reminders, and progress visualization

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Build habits with streaks, reminders, and progress visualization

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run habit-tracker`)
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
You are executing the habit-tracker workflow. Use the following context:

Description: Build habits with streaks, reminders, and progress visualization

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: habit-tracker
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Habit Tracker

Build lasting habits through conversation. Track streaks, get reminders, celebrate progress.

## What it does

Creates and tracks daily/weekly habits, maintains streak counts, sends optional reminders, and visualizes your progress over time. Simple accountability through your AI assistant.

## Usage

**Create habits:**
```
"New habit: meditate daily"
"Track reading 30 minutes"
"Add habit: gym 3x per week"
```

**Log completions:**
```
"Did meditation"
"Completed reading"
"Hit the gym today"
```

**Check progress:**
```
"How are my habits?"
"Meditation streak"
"Weekly habit summary"
```

**Set reminders:**
```
"Remind me to meditate at 7am"
"Habit reminder at 9pm"
```

## Habit Types

- **Daily**: Must complete every day for streak
- **Weekly**: Complete X times per week
- **Custom**: Define your own cadence

## Streak Rules

- Miss a day = streak resets (daily habits)
- Miss weekly target = week doesn't count
- Say "skip [habit] today" to pause without breaking streak (limited uses)

## Tips

- Start with 1-2 habits, add more as they stick
- Ask "habit insights" for pattern analysis
- Say "archive [habit]" to stop tracking without deleting history
- Morning check: "What habits do I need to do today?"
- All data stored locally

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
