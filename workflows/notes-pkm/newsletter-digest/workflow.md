# newsletter-digest

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jhillin8/newsletter-digest/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jhillin8/newsletter-digest/SKILL.md)
> Category: Notes & PKM

---

## Description

Summarize newsletters and articles, extract key insights, create reading lists

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Summarize newsletters and articles, extract key insights, create reading lists

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run newsletter-digest`)
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
You are executing the newsletter-digest workflow. Use the following context:

Description: Summarize newsletters and articles, extract key insights, create reading lists

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: newsletter-digest
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Newsletter Digest

Tame your inbox. Get AI summaries of newsletters and articles so you read what matters.

## What it does

Processes forwarded newsletters and linked articles, extracts key insights, creates prioritized reading lists, and learns your interests over time. Never miss important content, never drown in noise.

## Usage

**Summarize content:**
```
"Summarize this newsletter" [forward/paste]
"Digest https://article-url.com"
"What's important in my newsletters today?"
```

**Build reading lists:**
```
"Add to reading list: [url]"
"What's on my reading list?"
"Clear completed reads"
```

**Get insights:**
```
"Key takeaways from tech newsletters this week"
"Trending topics across my subscriptions"
"Compare viewpoints on [topic]"
```

**Manage preferences:**
```
"I'm interested in AI, fintech, productivity"
"Skip newsletters about marketing"
"Prioritize Stratechery"
```

## Features

- **Smart summaries**: Key points, not just shortened text
- **Topic extraction**: Tags and categorizes automatically
- **Cross-reference**: Finds related content across sources
- **Save for later**: Queue articles for focused reading time

## Tips

- Forward newsletters to Clawd for processing
- Say "brief" for 2-sentence summaries, "detailed" for deep analysis
- Ask "what did I miss this week?" for catch-up digest
- Works with any text content—not just newsletters

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
