# gita-sotd

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/apatki1996/gita-sotd/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/apatki1996/gita-sotd/SKILL.md)
> Category: Search & Research

---

## Description

Get the Bhagavad Gita Slok of the Day (SOTD) or fetch specific verses. Use when the user asks for a Gita verse, slok, daily wisdom from the Gita, Hindu scripture quotes, or anything related to the Bhagavad Gita text. Supports Sanskrit text, transliteration, and translations from multiple scholars.


**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Get the Bhagavad Gita Slok of the Day (SOTD) or fetch specific verses. Use when the user asks for a Gita verse, slok, daily wisdom from the Gita, Hindu scripture quotes, or anything related to the Bhagavad Gita text. Supports Sanskrit text, transliteration, and translations from multiple scholars.


### O - Orchestration
**Trigger:** User-invocable (via `aidarr run gita-sotd`)
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
You are executing the gita-sotd workflow. Use the following context:

Description: Get the Bhagavad Gita Slok of the Day (SOTD) or fetch specific verses. Use when the user asks for a Gita verse, slok, daily wisdom from the Gita, Hindu scripture quotes, or anything related to the Bhagavad Gita text. Supports Sanskrit text, transliteration, and translations from multiple scholars.


Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: gita-sotd
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Bhagavad Gita Slok of the Day

Fetch verses from the Bhagavad Gita using the free [vedicscriptures API](https://vedicscriptures.github.io/).

## Usage

Run the script to get a slok:

```bash
# Daily slok (deterministic, changes each day)
python3 scripts/fetch_slok.py

# Specific verse
python3 scripts/fetch_slok.py --chapter 2 --verse 47

# Random verse
python3 scripts/fetch_slok.py --random

# Different translator (prabhu, siva, purohit, gambir, chinmay, etc.)
python3 scripts/fetch_slok.py --translator siva

# Raw JSON output
python3 scripts/fetch_slok.py --json
```

## Available Translators

- `prabhu` - A.C. Bhaktivedanta Swami Prabhupada (default)
- `siva` - Swami Sivananda
- `purohit` - Shri Purohit Swami
- `gambir` - Swami Gambirananda
- `chinmay` - Swami Chinmayananda
- `tej` - Swami Tejomayananda (Hindi)
- `rams` - Swami Ramsukhdas (Hindi)
- `raman` - Sri Ramanuja

## Output Format

The script outputs formatted markdown with:

- Chapter and verse reference
- Sanskrit text (optional)
- Transliteration
- English/Hindi translation with author attribution

## API Reference

Base URL: `https://vedicscriptures.github.io`

- `GET /slok/:chapter/:verse` - Get specific verse
- `GET /chapter/:ch` - Get chapter info
- `GET /chapters` - List all chapters

The Bhagavad Gita has 18 chapters with 700 total verses.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
