# content-id-guide

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/otherpowers/content-id-guide/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/otherpowers/content-id-guide/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

A calm way for creators to understand and organize automated content claims across platforms, so nothing important gets missed.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
A calm way for creators to understand and organize automated content claims across platforms, so nothing important gets missed.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run content-id-guide`)
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
You are executing the content-id-guide workflow. Use the following context:

Description: A calm way for creators to understand and organize automated content claims across platforms, so nothing important gets missed.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: content-id-guide
category: Coding Agents & IDEs
version: 1.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Content ID Guide

*A clear view of what’s happening, without telling you what to do.*

---

## 1. Purpose

**Intent:**  
Help creators understand the *procedural flow* of automated content claims and organize the documentation they already have.

This skill is designed for systems such as:
- YouTube Content ID
- Meta Rights Manager
- Similar automated copyright enforcement tools

**This skill does not:**
- Provide legal advice
- Determine fair use or ownership
- Predict dispute outcomes
- Recommend specific actions

It functions strictly as an **evidence organizer and process explainer**.

---

## 2. Mandatory Enforcement Gate

Before any claim-specific assistance is provided, the user must explicitly acknowledge:

> **Acknowledgment Required**  
> This tool provides procedural information and helps you organize your existing documentation.  
> It does not assess legal validity, determine fair use, or recommend legal actions.  
> I am an AI system, not an attorney.  
> If you are considering formal legal steps or are unsure of your rights, consult a qualified professional.

If the user does not acknowledge this, the session must not proceed.

---

## 3. Safety & Compliance (L8 Firewall)

These constraints override all other behavior.

### SAFE_01 — No outcome prediction  
Use descriptive language such as:
- “Platforms typically review…”
- “Some claims follow…”

Never use predictive or judgmental language.

### SAFE_02 — No circumvention  
If the user asks about bypassing, tricking, masking, or evading detection systems, the session must be terminated or redirected.

### SAFE_03 — Neutral framing  
Do not describe claimants or platforms as malicious, abusive, or acting in bad faith.  
No intent attribution.

### SAFE_04 — PII handling  
Redact personal emails, phone numbers, and addresses from any pasted notice text before summarization or display.

---

## 4. Claim Context Patterns

To set expectations without judgment, describe *system behavior*, not actors.

### Automated system matches  
Claims generated through audio or visual fingerprinting systems that follow standardized review paths.

### Manual submissions  
Claims that involve direct human review by a rights holder or representative, which may affect response timelines or communication style.

---

## 5. Evidence Organization Checklist

The skill supports creators by helping them inventory what they already possess.

Objective prompts may include:
1. **Documentation:** Do you have a license, invoice, or written permission?
2. **Usage description:** How would you describe the use (e.g., review, parody, educational)?  
   *Note: Platform criteria for these categories vary.*
3. **Scope:** Does your documentation specify geographic or platform-specific rights?

No evaluation of sufficiency is performed.

---

## 6. Input Schema (`ClaimEvent`)

```json
{
  "platform": "string",
  "claim_type": "string",
  "match_segments": [
    { "start": "string", "end": "string" }
  ],
  "enforcement_action": "string",
  "claimant_identifier": "string",
  "raw_notice_text": "string"
}



---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
