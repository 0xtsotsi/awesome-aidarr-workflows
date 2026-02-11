# skillscanner

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/rexshang/skillscanner/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/rexshang/skillscanner/SKILL.md)
> Category: AI & LLMs

---

## Description

Security scanner for ClawHub skills from Gen Digital. Looks up skill safety via the scan API.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Security scanner for ClawHub skills from Gen Digital. Looks up skill safety via the scan API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run skillscanner`)
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
You are executing the skillscanner workflow. Use the following context:

Description: Security scanner for ClawHub skills from Gen Digital. Looks up skill safety via the scan API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: skillscanner
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# SkillScanner — Security Scanner for ClawHub Skills

> **"Trust, but verify."**

SkillScanner checks ClawHub skill safety by calling the scan API. You provide the skill URL; the API returns status and severity. Proceed only when the verdict is **SAFE**.

---

## How to Scan a Skill (Agent Instructions)

1. **Run the lookup** with the real skill URL (format: `https://clawhub.ai/author/skill-name`):

   ```bash
   curl --request POST --url "https://ai.gendigital.com/api/scan/lookup" \
     --header "Content-Type: application/json" \
     --data '{"skillUrl":"https://clawhub.ai/AUTHOR/SKILL_SLUG"}'
   ```

   Replace `AUTHOR` with actual author id and `SKILL_SLUG` with the actual skill identifier from the ClawHub URL.

2. **Interpret the response:**
   - **`status: "done"`** — Check the **`severity`** field for the verdict.
   - **`status: "analysis_pending"`** — The skill is awaiting manual review. Do not treat as safe; advise the user that the skill is pending review.

3. **Proceed or advise caution:**
   - **Proceed** only if **`severity` is `SAFE`**.
   - If severity is anything else (e.g. `WARNING`, `DANGEROUS`, `MALICIOUS`), **advise caution** and do not recommend using the skill until reviewed or cleared.

---

## Quick Start

```bash
# Example: scan a skill by its ClawHub URL
curl --request POST --url "https://ai.gendigital.com/api/scan/lookup" \
  --header "Content-Type: application/json" \
  --data '{"skillUrl":"https://clawhub.ai/author/skill-name"}'
```

Parse the JSON response: use `status` and `severity` as above.

---

## API Response Logic

| `status`           | Meaning              | Action |
|--------------------|----------------------|--------|
| `done`             | Scan complete        | Use `severity` for verdict (see below). |
| `analysis_pending` | Awaiting manual review | Advise that the skill is not yet cleared; do not treat as SAFE. |

| `severity` (when `status` = `done`) | Recommendation |
|-------------------------------------|----------------|
| **SAFE**                            | OK to proceed. |
| Any other value                     | Advise caution; do not recommend use until reviewed. |

---

## Why This Matters

Skills can run code and access your environment. Risks include:

| Risk | Impact |
|------|--------|
| **Execute arbitrary code** | Full system compromise |
| **Access your filesystem** | Data theft, ransomware |
| **Read environment variables** | API key theft |
| **Exfiltrate data via HTTP** | Privacy breach |
| **Install malicious dependencies** | Supply chain attack |

SkillScanner uses the scan API to help you decide whether to trust a skill before use.

---

## Limitations

- The API reflects the current backend verdict; obfuscated or novel threats may not be flagged.
- `analysis_pending` means human review has not yet concluded—treat as “unknown”, not safe.

Use alongside sandboxing, least privilege, and manual review when in doubt.

---

**Links:**
- [Agent Trust Hub](https://ai.gendigital.com)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
