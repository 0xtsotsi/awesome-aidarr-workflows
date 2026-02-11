# ui-ux-pro-max

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xobi667/ui-ux-pro-max/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xobi667/ui-ux-pro-max/SKILL.md)
> Category: Web & Frontend Development

---

## Description

UI/UX design intelligence and implementation guidance for building polished interfaces. Use when the user asks for UI design, UX flows, information architecture, visual style direction, design systems/tokens, component specs, copy/microcopy, accessibility, or to generate/critique/refine frontend UI (HTML/CSS/JS, React, Next.js, Vue, Svelte, Tailwind). Includes workflows for (1) generating new UI layouts and styling, (2) improving existing UI/UX, (3) producing design-system tokens and component guidelines, and (4) turning UX recommendations into concrete code changes.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
UI/UX design intelligence and implementation guidance for building polished interfaces. Use when the user asks for UI design, UX flows, information architecture, visual style direction, design systems/tokens, component specs, copy/microcopy, accessibility, or to generate/critique/refine frontend UI (HTML/CSS/JS, React, Next.js, Vue, Svelte, Tailwind). Includes workflows for (1) generating new UI layouts and styling, (2) improving existing UI/UX, (3) producing design-system tokens and component guidelines, and (4) turning UX recommendations into concrete code changes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run ui-ux-pro-max`)
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
You are executing the ui-ux-pro-max workflow. Use the following context:

Description: UI/UX design intelligence and implementation guidance for building polished interfaces. Use when the user asks for UI design, UX flows, information architecture, visual style direction, design systems/tokens, component specs, copy/microcopy, accessibility, or to generate/critique/refine frontend UI (HTML/CSS/JS, React, Next.js, Vue, Svelte, Tailwind). Includes workflows for (1) generating new UI layouts and styling, (2) improving existing UI/UX, (3) producing design-system tokens and component guidelines, and (4) turning UX recommendations into concrete code changes.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ui-ux-pro-max
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



Follow these steps to deliver high-quality UI/UX output with minimal back-and-forth.

## 1) Triage
Ask only what you must to avoid wrong work:
- Target platform: web / iOS / Android / desktop
- Stack (if code changes): React/Next/Vue/Svelte, CSS/Tailwind, component library
- Goal and constraints: conversion, speed, brand vibe, accessibility level (WCAG AA?)
- What you have: screenshot, Figma, repo, URL, user journey

If the user says "全部都要" (design + UX + code + design system), treat it as four deliverables and ship in that order.

## 2) Produce Deliverables (pick what fits)
Always be concrete: name components, states, spacing, typography, and interactions.

- **UI concept + layout**: Provide a clear visual direction, grid, typography, color system, key screens/sections.
- **UX flow**: Map the user journey, critical paths, error/empty/loading states, edge cases.
- **Design system**: Tokens (color/typography/spacing/radius/shadow), component rules, accessibility notes.
- **Implementation plan**: Exact file-level edits, component breakdown, and acceptance criteria.

## 3) Use Bundled Assets
This skill bundles data you can cite for inspiration/standards.

- **Design intelligence data**: Read from `skills/ui-ux-pro-max/assets/data/` when you need palettes, patterns, or UI/UX heuristics.
- **Upstream reference**: If you need more phrasing/examples, consult `skills/ui-ux-pro-max/references/upstream-skill-content.md`.

## 4) Optional Script (Design System Generator)
If you need to quickly generate tokens and page-specific overrides, use the bundled script:

```bash
python3 skills/ui-ux-pro-max/scripts/design_system.py --help
```

Prefer running it when the user wants a structured token output (ASCII-friendly).

## Output Standards
- Default to ASCII-only tokens/variables unless the project already uses Unicode.
- Include: spacing scale, type scale, 2-3 font pair options, color tokens, component states.
- Always cover: empty/loading/error, keyboard navigation, focus states, contrast.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
