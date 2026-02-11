# researchassistant

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/eksubin/researchassistant/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/eksubin/researchassistant/SKILL.md)
> Category: Search & Research

---

## Description

Monitors research topics for new papers, conferences, and journals.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Monitors research topics for new papers, conferences, and journals.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run researchassistant`)
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
You are executing the researchassistant workflow. Use the following context:

Description: Monitors research topics for new papers, conferences, and journals.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: researchassistant
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# ResearchMonitor

This skill helps you keep the user updated on their specific research field.

## Workflow

1.  **Check Configuration**:
    -   Read `research_config.json` in this directory to find the user's research topics and last checked date.
    -   If the file doesn't exist or topics are empty, ask the user what research topics they are interested in and save them using `scripts/daily_briefing.py --add-topic "topic"`.

2.  **Daily Check**:
    -   Get the current date.
    -   Compare with `last_checked` in `research_config.json`.
    -   If already checked today, do nothing unless explicitly asked.

3.  **Perform Search**:
    -   For each topic, use `search_web` to look for:
        -   "new research papers [topic] [current month/year]"
        -   "upcoming conferences [topic] [current year]"
        -   "new journal issues [topic] [current month/year]"
        -   Check specialized platforms like arXiv, IEEE Xplore, Google Scholar (via web search), or X (Twitter) if relevant.

4.  **Filter & Analyze**:
    -   For each potential item found, use `scripts/daily_briefing.py --check-seen "URL or Unique Title"`.
    -   If it returns "true", SKIP IT.
    -   Compare found items with what might have been seen yesterday (this requires some memory or just checking if the publication date is very recent, e.g., last 24-48 hours).
    -   **CRITICAL**: If there is *nothing significantly new* (no new major papers, no new conference announcements), **DO NOT BOTHER THE USER**.

5.  **Report**:
    -   If new items are found, compile a brief markdown report.
    -   Include:
        -   **Title**: News/Paper Title
        -   **Source**: URL/Journal Name
        -   **Summary**: 1-sentence summary of why it's relevant.
    -   Present this to the user.
    -   Mark the items as seen using `scripts/daily_briefing.py --mark-seen "URL or Unique Title"`.
    -   Update the `last_checked` date using `scripts/daily_briefing.py --update-date`.

## Scripts

-   `python scripts/daily_briefing.py --add-topic "topic"`: Adds a new research topic.
-   `python scripts/daily_briefing.py --list-topics`: Lists current topics.
-   `python scripts/daily_briefing.py --update-date`: Updates the last checked timestamp to now.
-   `python scripts/daily_briefing.py --check-seen "ID"`: Checks if an item ID (URL/Title) is already in memory.
-   `python scripts/daily_briefing.py --mark-seen "ID"`: Marks an item ID as seen.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
