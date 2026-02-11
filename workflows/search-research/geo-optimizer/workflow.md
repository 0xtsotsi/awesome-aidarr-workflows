# geo-optimizer

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/artyomx33/geo-optimizer/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/artyomx33/geo-optimizer/SKILL.md)
> Category: Search & Research

---

## Description

Optimize content for AI citation (GEO). Use when user says "GEO", "generative engine optimization", "AI citation", "get cited by AI", "AI-friendly content", or creating content for ChatGPT/Claude/Perplexity visibility.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Optimize content for AI citation (GEO). Use when user says "GEO", "generative engine optimization", "AI citation", "get cited by AI", "AI-friendly content", or creating content for ChatGPT/Claude/Perplexity visibility.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run geo-optimizer`)
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
You are executing the geo-optimizer workflow. Use the following context:

Description: Optimize content for AI citation (GEO). Use when user says "GEO", "generative engine optimization", "AI citation", "get cited by AI", "AI-friendly content", or creating content for ChatGPT/Claude/Perplexity visibility.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: geo-optimizer
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# GEO Content Optimizer

## When To Use
- Creating content for AI citation
- Refactoring articles for AI compatibility
- Improving quotability for AI responses
- Competing in AI-first search
- Adding authority signals AI systems recognize

## Core Concept
**SEO** = Rank in search results
**GEO** = Get cited in AI-generated answers

## The 8 GEO Dimensions

| Dimension | Low (1-2) | High (4-5) |
|-----------|-----------|------------|
| Definition Clarity | Vague | Citable definitions with metrics |
| Quotable Statements | Generic claims | Specific facts with sources |
| Factual Density | Opinion-heavy | Data-packed |
| Source Citations | None | Traceable to authority |
| Q&A Format | Prose only | Explicit Q&A sections |
| Authority Signals | No credentials | Expert bylines, credentials |
| Content Freshness | Outdated | Dated citations, recent data |
| Structural Clarity | Poor hierarchy | Clear headers, lists, tables |

## The GEO Score
Score each dimension 1-5. Total /40:
- 32-40: AI-ready
- 24-31: Needs optimization
- 16-23: Major work needed

## Quick Wins (30-minute edits)

1. Add specific statistics with dates and sources
2. Create standalone definition paragraphs
3. Include expert quotes with credentials
4. Add comparison tables
5. Create FAQ section with 5-7 questions
6. Replace vague claims with verified facts
7. Insert authoritative source citations

## Output Format

```markdown
## GEO Audit
Current Score: [X]/40

### Dimension Scores
| Dimension | Score | Quick Fix |
|-----------|-------|-----------|
| [dimension] | [1-5] | [action] |

## Optimized Content Sections

### Definition (Citable)
[Term] is [category] that [function], [key metric].

### Key Statistics
- [Stat with source and date]
- [Stat with source and date]

### FAQ Section
**Q: [Common question]?**
A: [Direct, quotable answer with citation]
```

## Integration
Compounds with:
- **app-planning-skill** → Plan content strategy
- **writing-plans** → Structure content projects

---
See references/dimensions.md for scoring details
See references/patterns.md for optimization patterns
See references/examples.md for before/after examples

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
