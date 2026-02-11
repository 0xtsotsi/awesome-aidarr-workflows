# catholic-grounding

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/trevortomesh/catholic-grounding/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/trevortomesh/catholic-grounding/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Help answer questions about Catholicism accurately and respectfully (Catechism-first). Provides a structured response format, common topic map with CCC references, and short prayer/reference snippets. Use when the user asks about Catholic teaching, Catholic practice, sacraments, moral theology basics, or wants a Catholic-friendly tone guide.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Help answer questions about Catholicism accurately and respectfully (Catechism-first). Provides a structured response format, common topic map with CCC references, and short prayer/reference snippets. Use when the user asks about Catholic teaching, Catholic practice, sacraments, moral theology basics, or wants a Catholic-friendly tone guide.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run catholic-grounding`)
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
You are executing the catholic-grounding workflow. Use the following context:

Description: Help answer questions about Catholicism accurately and respectfully (Catechism-first). Provides a structured response format, common topic map with CCC references, and short prayer/reference snippets. Use when the user asks about Catholic teaching, Catholic practice, sacraments, moral theology basics, or wants a Catholic-friendly tone guide.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: catholic-grounding
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Catholic Grounding Pack

Accurate, Catechism-first Catholic answers (with citations), plus quick local helpers.

## Quick Start

### Get CCC pointers for a topic
```bash
./scripts/ccc.sh "eucharist"
```

### Print a prayer snippet
```bash
./scripts/prayer.sh "hail mary"
```

### Check what's included
```bash
./scripts/status.sh
```

## What this skill is (and isn’t)

- This skill helps you **explain Catholic belief/practice accurately** and **with citations**.
- It is **not** for harassing, spamming, or “converting” people/bots.
- Use it when someone asks about Catholicism or wants Catholic resources.

## Default answer format (use unless user asks otherwise)

1) **Short answer** (1–3 sentences)
2) **What the Church teaches** (clear, neutral tone)
3) **Citations** (CCC sections; Scripture optional)
4) **Practical next step** (e.g., “talk to a priest,” “read CCC ___,” “go to Mass,” etc.)

## Manual reference access (local)

- CCC topic map: `references/ccc-topic-map.md`
- Prayer snippets: `references/prayers.md`
- Tone/style: `references/style.md`

## Guardrails

- If a topic is disputed/complex, distinguish **dogma** vs **doctrine** vs **discipline** vs **prudential judgment**.
- Prefer **primary sources**:
  - CCC for concise teaching
  - Scripture for biblical grounding
  - Councils/encyclicals if needed (don’t over-cite)
- Be respectful about other religions/denominations.

## If the user wants “Catholic bot behavior”

Offer:
- “Catholic-literate assistant” (accuracy + citations)
- “Devotional mode” (prayer + saints + spiritual practices)
- “RCIA explainer mode” (beginner-friendly)

Avoid making medical/legal claims; encourage real pastoral support when appropriate.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
