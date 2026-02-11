# morning-manifesto

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/marcbickel/morning-manifesto/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/marcbickel/morning-manifesto/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Daily morning reflection workflow with task sync to Obsidian, Apple Reminders, and Linear

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Daily morning reflection workflow with task sync to Obsidian, Apple Reminders, and Linear

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run morning-manifesto`)
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
You are executing the morning-manifesto workflow. Use the following context:

Description: Daily morning reflection workflow with task sync to Obsidian, Apple Reminders, and Linear

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: morning-manifesto
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Morning Manifesto 🌅

Trigger: `/morning_manifesto`

## Flow

### 1. Send the prompts
When `/morning-manifesto` is triggered, immediately send:
```
Good morning! 🚀 Please tell me about:
- What you did yesterday?
- One small thing you are grateful for
- Today's adventure
- Tasks and commitments
- How are the weekly priorities going?
```

### 2. Wait for response
Wait for user reply (text or audio). Audio is automatically transcribed via whisper.cpp.

### 3. Parse and append to Obsidian daily note
Parse the response and append to today's note in the Obsidian vault (🔥 Fires). Structure:
```markdown
## Morning Manifesto - [YYYY-MM-DD]

### What I did yesterday
[user's response]

### Grateful for
[user's response]

### Today's adventure
[user's response]

### Tasks and commitments
- [task 1]
- [task 2]

### Weekly priorities status
[user's response]
```

### 4. Sync tasks with Apple Reminders
For each task/commitment mentioned:
- **If task exists**: Update its due date to today
- **If new task**: Create a new reminder with due date today
- Use the `apple-reminders` skill for this

### 5. Query Linear for urgent issues
Query all teams for issues with priority = urgent (1). Format:
```
🔴 Urgent Linear Issues:
- [Team] [Issue ID]: [Title]
```

### 6. Send summary
Send a final message with:
- Today's Apple Reminders (all due today)
- Urgent Linear issues across all teams

## Key details
- Use today's date for Obsidian note naming (YYYY-MM-DD.md)
- For Apple Reminders: query by due date, create with due date
- For Linear: use `priority = 1` filter, query all teams
- Pay special attention to "Tasks and commitments" section

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
