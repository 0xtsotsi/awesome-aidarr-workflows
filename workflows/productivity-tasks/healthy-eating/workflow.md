# healthy-eating

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jhillin8/healthy-eating/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jhillin8/healthy-eating/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Build healthy eating habits with meal logging, nutrition tracking, and food choices

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Build healthy eating habits with meal logging, nutrition tracking, and food choices

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run healthy-eating`)
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
You are executing the healthy-eating workflow. Use the following context:

Description: Build healthy eating habits with meal logging, nutrition tracking, and food choices

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: healthy-eating
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Healthy Eating

Build sustainable nutrition habits through simple meal logging and mindful food choices.

## What it does

Log meals without obsession. Get real-time nutrition awareness. Receive personalized suggestions for healthier choices. Track patterns over time and build habits that stick—no calorie counting required.

## Usage

**Log meals**
- Record what you ate and when
- Capture portion sizes and meal context (breakfast, snack, lunch, dinner)
- Notes on how you felt after eating

**Get suggestions**
- Ask for healthy meal ideas based on ingredients you have
- Get quick swaps for favorite foods
- Receive context-aware recommendations (late night, busy day, social event)

**Check nutrition**
- View nutrient breakdown: proteins, fats, carbs, fiber, micronutrients
- Understand food quality and satiety impact
- See hydration status and daily totals

**Meal planning**
- Plan weekly meals with minimal friction
- Balance macros and whole foods naturally
- Batch prep suggestions for busy schedules

**Track habits**
- View eating patterns over days and weeks
- Spot triggers and improvements
- Celebrate consistency milestones

## Food Categories

**Proteins**
Lean meats, fish, eggs, legumes, nuts, seeds, Greek yogurt

**Vegetables**
Leafy greens, cruciferous, root veggies, colorful variety

**Whole grains**
Oats, brown rice, quinoa, whole wheat, barley

**Healthy fats**
Olive oil, avocados, fatty fish, nuts, seeds

**Hydration**
Water, herbal tea, electrolyte balance

## Tips

- Log immediately after eating—memory fades but patterns stick
- Focus on food quality and how your body feels, not numbers on a screen
- Pair proteins with veggies at every meal to stabilize energy and hunger
- Plan meals on Sundays so weekday choices default to healthy options
- All data stays local on your machine


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
