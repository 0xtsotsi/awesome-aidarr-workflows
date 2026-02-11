# zettelkasten

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/rainy-cogmet/zettelkasten/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/rainy-cogmet/zettelkasten/SKILL.md)
> Category: Notes & PKM

---

## Description

Zettelkasten - Card box note taking system with AI insights

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Zettelkasten - Card box note taking system with AI insights

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run zettelkasten`)
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
You are executing the zettelkasten workflow. Use the following context:

Description: Zettelkasten - Card box note taking system with AI insights

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: zettelkasten
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Zettelkasten Card Box System

## Description
A complete implementation of the Zettelkasten note-taking method, featuring:
- Idea capture and organization
- AI-generated insights and suggestions
- Automatic connection detection
- Daily review capabilities

## Usage

### Record Idea
```
Record Idea: [Your idea content here]
```

Example:
```
Record Idea: I found that meditating 10 minutes daily improves focus and sleep quality
```

## Features
1. **Idea Capture**: Automatically generates structured cards with metadata
2. **AI Insights**: Provides extended suggestions and research directions
3. **Connection Detection**: Finds relationships between different ideas
4. **Daily Review**: Random card review for knowledge consolidation

## Output Format
```markdown
---
ID: [timestamp]
Tags: #tag1 #tag2 #tag3
Type: Flash
Date: [date]
---

## [Title]
[Content]

> AI Insight: [Generated insight]
```
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
