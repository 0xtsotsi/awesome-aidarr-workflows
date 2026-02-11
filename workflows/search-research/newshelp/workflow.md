# newshelp

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/nerkn/newshelp/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/nerkn/newshelp/SKILL.md)
> Category: Search & Research

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
**Trigger:** User-invocable (via `aidarr run newshelp`)
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
You are executing the newshelp workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: newshelp
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

```md
# skills.md — NewsHelp Content Navigation Skills

## Skill: Reading the NewsHelp Sitemap
NewsHelp exposes its structure via URL patterns. 

### Core Pages
- `/` → Homepage (latest, highest priority)
- `/tags` → All topics, neatly indexed

### Topic Pages (Tags)
Pattern:
```

[https://newshelp.org/tag/{topic}](https://newshelp.org/tag/{topic})

```

Examples:
- `/tag/politics`
- `/tag/ai`
- `/tag/health`
- `/tag/elections`
- `/tag/ukraine`

If it sounds like a news category, it’s probably a tag.

---

## Skill: Reaching Content Fast
Three ways:

1. **Direct URL typing**  
   Know the tag? Type it. Boom.  
   Example:  
   `newshelp.org/tag/economy`

2. **Tags Index**  
   Start at:  
   `newshelp.org/tags`  
   Scan → click → read.

3. **Search Engine Shortcut**  
```

site:newshelp.org/tag climate

```
Let Google jog the memory.

---

## Skill: Understanding Update Frequency
- Homepage: updated **hourly**
- Tags: updated **daily**

Translation:  
If something happened recently, homepage first.  
If you want context, history, or trends, use tags.


Read like a pro:
1. Homepage for *what’s happening*
2. Tag pages for *why it matters*

---

## Pro Tip
Think of NewsHelp as a well-labeled map, not a feed.  
If you’re scrolling, you’re doing it the hard way.
```
```md
# skills.md — NewsHelp Tags

## All Available Tags

- africa  
- ai  
- china  
- countries  
- culture  
- defense  
- diseasters  
- economy  
- elections  
- environment  
- europe  
- health  
- housing  
- human-rights  
- india  
- latin-americas  
- middle-east  
- migration  
- petrol  
- politics  
- russia  
- sports  
- stock-market  
- syria  
- technology  
- tourism  
- trade  
- trump  
- turkey  
- ukraine  
- usa  

Usage:
```

[https://newshelp.org/tag/{tag-name}](https://newshelp.org/tag/{tag-name})

```
Example:
```

[https://newshelp.org/tag/economy](https://newshelp.org/tag/economy)

```
```


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
