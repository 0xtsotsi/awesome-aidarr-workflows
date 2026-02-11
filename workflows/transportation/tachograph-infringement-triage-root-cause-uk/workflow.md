# tachograph-infringement-triage-root-cause-uk

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kowl64/tachograph-infringement-triage-root-cause-uk/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kowl64/tachograph-infringement-triage-root-cause-uk/SKILL.md)
> Category: Transportation

---

## Description

Triages tachograph infringements, identifies common patterns, and outputs “what to check next” prompts and weekly review notes. USE WHEN doing weekly tacho/WTD reviews.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Triages tachograph infringements, identifies common patterns, and outputs “what to check next” prompts and weekly review notes. USE WHEN doing weekly tacho/WTD reviews.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tachograph-infringement-triage-root-cause-uk`)
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
You are executing the tachograph-infringement-triage-root-cause-uk workflow. Use the following context:

Description: Triages tachograph infringements, identifies common patterns, and outputs “what to check next” prompts and weekly review notes. USE WHEN doing weekly tacho/WTD reviews.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tachograph-infringement-triage-root-cause-uk
category: Transportation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Tachograph Triage & Root-Cause Prompts (UK)

## PURPOSE
Run a weekly review workflow that turns infringement outputs into clear triage notes, root-cause prompts, and “what to check next” steps.

## WHEN TO USE
- “Do a weekly tacho and WTD compliance review for these drivers.”
- “Triage these infringements and tell me what to check next.”
- “Summarise this PDF infringement report into actions and driver follow-ups.”

DO NOT USE WHEN…
- You only need a single driver-facing message (use the infringement coach skill).
- You want general rule explanations without records.

## INPUTS
- REQUIRED:
  - Driver list + date range
  - Infringement summaries (CSV/PDF extract or pasted lines)
- OPTIONAL:
  - Any known operational context (routes, delays, multi-drop, ferry/train, staffing)
  - Prior RAG history
- EXAMPLES:
  - “Drivers A–F, last week’s infringement PDF attached; need weekly pack.”

## OUTPUTS
- `weekly-tacho-wtd-review.md` (manager-facing)
- `triage-actions-by-driver.md`
- Success criteria:
  - Clear “next checks” per infringement type
  - Flags where investigation/discipline thresholds may be approaching (per your policy)

## WORKFLOW
1. Confirm period and driver list.
   - IF missing → **STOP AND ASK THE USER**.
2. Normalise infringements into a per-driver list (facts only).
3. Pattern scan using `references/common-infringement-patterns.md`.
4. For each driver, generate:
   - Likely root-cause prompts (questions to ask, operational checks)
   - “What to check next” steps using `assets/what-to-check-next-playbook.md`
5. Produce weekly pack using `assets/weekly-review-pack-template.md`.
6. If RAG escalation depends on missing history → **STOP AND ASK THE USER** for counts/outcomes.

## OUTPUT FORMAT
```text
# triage-actions-by-driver.md
Period:
Sources:

## Driver [X]
Infringements (facts):
- …

What to check next:
- …

Root-cause prompts:
- …

Proposed follow-up:
- Coaching / monitoring / investigation trigger (per policy)
```

## SAFETY & EDGE CASES
- If records appear incomplete (missing days, download gaps), flag as a risk/gap rather than guessing why.
- Avoid blame language; keep triage neutral.

## EXAMPLES
- Input: “Weekly review for 12 drivers”
  - Output: weekly pack + per-driver triage actions and check-next prompts

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
