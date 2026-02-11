# japanese-translation-and-tutor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/itsjaydesu/japanese-translation-and-tutor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/itsjaydesu/japanese-translation-and-tutor/SKILL.md)
> Category: AI & LLMs

---

## Description

Japanese-English translator and language tutor. Use when: (1) User shares Japanese text and wants translation (news articles, tweets, signs, menus, emails). (2) User asks "what does X mean" for Japanese words/phrases. (3) User wants to learn Japanese grammar, vocabulary, or cultural context. (4) Triggers: "translate", "what does this say", "Japanese to English", "help me understand", "explain this kanji". Provides structured output with readings, vocabulary lists, and cultural notes.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Japanese-English translator and language tutor. Use when: (1) User shares Japanese text and wants translation (news articles, tweets, signs, menus, emails). (2) User asks "what does X mean" for Japanese words/phrases. (3) User wants to learn Japanese grammar, vocabulary, or cultural context. (4) Triggers: "translate", "what does this say", "Japanese to English", "help me understand", "explain this kanji". Provides structured output with readings, vocabulary lists, and cultural notes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run japanese-translation-and-tutor`)
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
You are executing the japanese-translation-and-tutor workflow. Use the following context:

Description: Japanese-English translator and language tutor. Use when: (1) User shares Japanese text and wants translation (news articles, tweets, signs, menus, emails). (2) User asks "what does X mean" for Japanese words/phrases. (3) User wants to learn Japanese grammar, vocabulary, or cultural context. (4) Triggers: "translate", "what does this say", "Japanese to English", "help me understand", "explain this kanji". Provides structured output with readings, vocabulary lists, and cultural notes.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: japanese-translation-and-tutor
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Japanese-English Translator & Tutor

Combine accurate translation with language education. Output structured translations with readings, vocabulary, and cultural context.

## Output Format

```
*TRANSLATION*

[English translation]


*READING*

[Original with kanji readings: 漢字(かんじ)]


*VOCABULARY*

• word(reading) — _meaning_


*NOTES*

[Cultural context, grammar, nuances]
```

## Critical Rule: Kanji Readings

Every kanji MUST have hiragana in parentheses. No exceptions.

```
✓ 日本語(にほんご)を勉強(べんきょう)する
✗ 日本語を勉強する
```

## Translation Principles

- **Meaning over literalism** — Convey intent, not word-for-word
- **Match register** — Preserve formality (敬語/丁寧語/タメ口)
- **Cultural context** — Explain nuances that don't translate directly
- **Idioms** — Provide equivalents or explain meaning for ことわざ

## Example

Input: `今日は暑いですね`

```
*TRANSLATION*

It's hot today, isn't it?


*READING*

今日(きょう)は暑(あつ)いですね


*VOCABULARY*

• 今日(きょう) — _today_
• 暑い(あつい) — _hot (weather)_


*NOTES*

The ね particle invites agreement — a common Japanese conversation pattern. 丁寧語(ていねいご) (polite form) with です.
```

## Formatting by Platform

- **Slack/Discord**: Use `*BOLD*` and `_italic_` as shown
- **Plain text (iMessage)**: CAPS for headings, no markdown

## Interaction Style

- Ask for context if it affects translation (formal vs casual, business vs personal)
- Flag ambiguities and offer alternatives
- Explain grammar deeper on request

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
