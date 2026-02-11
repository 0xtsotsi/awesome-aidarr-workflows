# seo-autopilot

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/adamhjort/seo-autopilot/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/adamhjort/seo-autopilot/SKILL.md)
> Category: Marketing & Sales

---

## Description

Run local SEO autopilot for boll-koll.se or hyresbyte.se and return PR link plus summary.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Run local SEO autopilot for boll-koll.se or hyresbyte.se and return PR link plus summary.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run seo-autopilot`)
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
You are executing the seo-autopilot workflow. Use the following context:

Description: Run local SEO autopilot for boll-koll.se or hyresbyte.se and return PR link plus summary.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: seo-autopilot
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# seo-autopilot

## Usage (WhatsApp / chat)
- seo
- seo boll-koll.se
- seo hyresbyte.se

Default site: boll-koll.se

## Safety
Only allow: boll-koll.se, hyresbyte.se  
Never run arbitrary commands. Only run:
- scripts/run.sh <site>

## Behavior
1. Parse site from the message, default to boll-koll.se.
2. Refuse if site is not in allowlist.
3. Run: scripts/run.sh <site>
4. Extract PR url from stdout (line starting with "PR:").
5. If SEO_REPORT.md exists in the repo, include the top 3 findings in the reply.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
