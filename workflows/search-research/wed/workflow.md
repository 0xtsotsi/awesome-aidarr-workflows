# wed

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/orlyjamie/wed/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/orlyjamie/wed/SKILL.md)
> Category: Search & Research

---

## Description

Security awareness demo - demonstrates supply chain risks in AI coding assistants. See the full research: https://x.com/theonejvo/status/2015892980851474595

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Security awareness demo - demonstrates supply chain risks in AI coding assistants. See the full research: https://x.com/theonejvo/status/2015892980851474595

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run wed`)
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
You are executing the wed workflow. Use the following context:

Description: Security awareness demo - demonstrates supply chain risks in AI coding assistants. See the full research: https://x.com/theonejvo/status/2015892980851474595

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: wed
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# What Would Elon Do? (WED)

## This is a Security Research Demo

This skill was created as part of security research demonstrating supply chain vulnerabilities in AI coding assistant ecosystems.

**Read the full research thread:** https://x.com/theonejvo/status/2015892980851474595

## What This Demonstrates

1. **Download counts can be trivially inflated** - Don't trust popularity metrics
2. **Skills can execute arbitrary code** - Always read the source before installing
3. **Social engineering works** - A catchy name got you here

## Is This Malicious?

No. This is a **neutered demo version**:
- NO commands are executed
- NO data is collected
- NO network requests are made

The original research PoC only sent an anonymous ping to count executions - no user data was ever collected.

## Protect Yourself

1. **ALWAYS read SKILL.md and source files before installing**
2. **Don't trust download counts or stars** - they can be faked
3. **Be suspicious of skills that seem too good to be true**

---

**Research by:** [@theonejvo](https://x.com/theonejvo)

**Full writeup:** https://x.com/theonejvo/status/2015892980851474595

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
