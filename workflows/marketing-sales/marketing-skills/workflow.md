# marketing-skills

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jchopard69/marketing-skills/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jchopard69/marketing-skills/SKILL.md)
> Category: Marketing & Sales

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
**Trigger:** User-invocable (via `aidarr run marketing-skills`)
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
You are executing the marketing-skills workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: marketing-skills
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Marketing Skills

## Summary

One installed skill containing 23 marketing modules. Pick the relevant module under `references/` to get practical checklists, frameworks, and copy/paste deliverables.

This skill vendors the full content from `coreyhaines31/marketingskills` under `references/` and provides a simple router to load the right module.

## How to use

1) Identify the module that matches the request.
2) Read the corresponding `references/<module>/SKILL.md` file.
3) Apply the framework and deliver practical outputs (drafts + checklists).

## Included modules (what each one does)

Each module lives at `references/<module>/SKILL.md`.

- `ab-test-setup`: plan and implement A/B tests
- `analytics-tracking`: set up tracking and measurement (GA4/GTM/events)
- `competitor-alternatives`: competitor comparison + alternatives / “vs” pages
- `copy-editing`: edit and polish existing copy
- `copywriting`: write or improve marketing copy (headlines, CTAs, page copy)
- `email-sequence`: build email sequences and drip campaigns
- `form-cro`: optimize lead capture and contact forms
- `free-tool-strategy`: plan engineering-as-marketing free tools (calculators, generators)
- `launch-strategy`: product launches and announcements
- `marketing-ideas`: idea bank for growth + marketing tactics
- `marketing-psychology`: mental models / cognitive biases for better persuasion
- `onboarding-cro`: improve activation and onboarding
- `page-cro`: conversion optimization for any marketing page
- `paid-ads`: create and optimize paid ad campaigns
- `paywall-upgrade-cro`: optimize in-app paywalls and upgrade screens
- `popup-cro`: create/optimize popups and modals
- `pricing-strategy`: pricing, packaging, and monetization
- `programmatic-seo`: build SEO pages at scale (templates + data)
- `referral-program`: design referral and affiliate programs
- `schema-markup`: add structured data and rich snippets
- `seo-audit`: audit technical and on-page SEO
- `signup-flow-cro`: optimize signup and registration flows
- `social-content`: create and schedule social media content

## Module router

Pick one of these modules and read the matching file:

- `references/page-cro/SKILL.md`
- `references/signup-flow-cro/SKILL.md`
- `references/onboarding-cro/SKILL.md`
- `references/form-cro/SKILL.md`
- `references/popup-cro/SKILL.md`
- `references/paywall-upgrade-cro/SKILL.md`
- `references/copywriting/SKILL.md`
- `references/copy-editing/SKILL.md`
- `references/email-sequence/SKILL.md`
- `references/social-content/SKILL.md`
- `references/analytics-tracking/SKILL.md`
- `references/ab-test-setup/SKILL.md`
- `references/seo-audit/SKILL.md`
- `references/programmatic-seo/SKILL.md`
- `references/schema-markup/SKILL.md`
- `references/competitor-alternatives/SKILL.md`
- `references/pricing-strategy/SKILL.md`
- `references/launch-strategy/SKILL.md`
- `references/paid-ads/SKILL.md`
- `references/referral-program/SKILL.md`
- `references/free-tool-strategy/SKILL.md`
- `references/marketing-ideas/SKILL.md`
- `references/marketing-psychology/SKILL.md`

## Output rules

- Prefer 80/20: biggest levers first.
- Never invent metrics or keyword volumes. If missing, label assumptions.
- When possible: include copy/paste drafts and an implementation checklist.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
