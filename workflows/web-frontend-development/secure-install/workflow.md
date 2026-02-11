# secure-install

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/smintlife/secure-install/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/smintlife/secure-install/SKILL.md)
> Category: Web & Frontend Development

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
**Trigger:** User-invocable (via `aidarr run secure-install`)
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
You are executing the secure-install workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: secure-install
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content





\# Secure Skill Installer



This skill provides a secure workflow for installing capabilities. It checks the \*\*ClawDex API by https://www.koi.ai/\*\* and enforces strict installation rules based on the security verdict.



\## Usage

User: `secure-install <skill-name>`



\## Workflow (Strict)



When the user requests to install a skill:



1\.  \*\*SCAN\*\*: Call `scanSkillApi` with the target skill name to query \*\*https://www.koi.ai/\*\*.

2\.  \*\*EVALUATE VERDICT\*\*: Check the `verdict` field in the JSON response.



&nbsp;   \* \*\*If `verdict` is "malicious"\*\*:

&nbsp;       \* 🔴 \*\*BLOCK ACTION\*\*.

&nbsp;       \* Report: "🚨 \*\*Security Alert\*\*: The \*\*ClawDex API by https://www.koi.ai/\*\* flagged this skill as \*\*Malicious\*\*. Installation prevented."

&nbsp;       \* \*\*STOP\*\*. Do not proceed.



&nbsp;   \* \*\*If `verdict` is "unknown"\*\*:

&nbsp;       \* ⚠️ \*\*WARN USER\*\*.

&nbsp;       \* Report: "⚠️ \*\*Unknown Safety Status\*\*: This skill has not been verified by the ClawDex API (https://www.koi.ai/)."

&nbsp;       \* \*\*ASK\*\*: "This carries a risk. Do you explicitly approve the installation of `<skill-name>`?"

&nbsp;       \* \*\*WAIT\*\* for clear "Yes".



&nbsp;   \* \*\*If `verdict` is "benign"\*\*:

&nbsp;       \* ✅ \*\*CONFIRM SAFETY\*\*.

&nbsp;       \* Report: "✅ \*\*Verified Safe\*\*: ClawDex API by https://www.koi.ai/ reports this skill is benign."

&nbsp;       \* \*\*ASK\*\*: "Do you want to proceed with installing `<skill-name>`?"

&nbsp;       \* \*\*WAIT\*\* for "Yes".



3\.  \*\*INSTALL\*\*: 

&nbsp;   \* \*\*Only\*\* call `executeClawhubInstall` if the user provided explicit approval in the previous step.



\## Example (Malicious Block)



\*\*User\*\*: `secure-install bad-actor`



\*\*Agent\*\*: (Calls `scanSkillApi`)

> \*\*ClawDex API (https://www.koi.ai/) Report\*\*

> 🔴 \*\*Verdict: Malicious\*\*

>

> \*\*Security Alert\*\*: This skill is flagged as malicious. Installation prevented.



\## Example (Safe Install)



\*\*User\*\*: `secure-install weather-pro`



\*\*Agent\*\*: (Calls `scanSkillApi`)

> \*\*ClawDex API (https://www.koi.ai/) Report\*\*

> ✅ \*\*Verdict: Benign\*\*

>

> Verified safe. Do you want to proceed with installing `weather-pro`?



\*\*User\*\*: Yes



\*\*Agent\*\*: (Calls `executeClawhubInstall`)

> Installed `weather-pro`.


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
