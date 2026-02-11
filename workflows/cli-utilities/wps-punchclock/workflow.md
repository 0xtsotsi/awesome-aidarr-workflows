# wps-punchclock

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dxh141130/wps-punchclock/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dxh141130/wps-punchclock/SKILL.md)
> Category: CLI Utilities

---

## Description

Automate punching time in/out on WPS Time / NetTime (wpstime.com NetTime). Use for phrases like setup punchclock/configure punchclock/set up time clock, clock in/clock out, start break/end break, start lunch/end lunch, check status/status. Runs a Playwright flow, captures a screenshot, and replies with a brief confirmation.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Automate punching time in/out on WPS Time / NetTime (wpstime.com NetTime). Use for phrases like setup punchclock/configure punchclock/set up time clock, clock in/clock out, start break/end break, start lunch/end lunch, check status/status. Runs a Playwright flow, captures a screenshot, and replies with a brief confirmation.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run wps-punchclock`)
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
You are executing the wps-punchclock workflow. Use the following context:

Description: Automate punching time in/out on WPS Time / NetTime (wpstime.com NetTime). Use for phrases like setup punchclock/configure punchclock/set up time clock, clock in/clock out, start break/end break, start lunch/end lunch, check status/status. Runs a Playwright flow, captures a screenshot, and replies with a brief confirmation.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: wps-punchclock
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# WPS Time / NetTime Punchclock

Run the bundled Playwright script to log into WPS Time NetTime using macOS Keychain credentials, perform the requested punch action (or status check), take a screenshot, and report results.

## Inputs → actions
Map user intent to the script `--action`:

### Setup / credentials
- setup punchclock / configure punchclock / set up time clock → run setup flow

### Punch actions
- clock in → `clock-in`
- clock out → `clock-out`
- start break → `start-break`
- end break → `end-break` (implemented as `Clock In (end break)` in script)
- start lunch → `start-lunch`
- end lunch → `end-lunch` (implemented as `Clock In (end lunch)` in script)
- status / check status → `status`

## First-time setup (per machine / per user)

### Option A (recommended): local terminal setup (password never enters chat logs)
Run the interactive setup script to store credentials in **macOS Keychain**:

```bash
cd {baseDir}/scripts
node ./setup.mjs
```

This stores credentials locally under Keychain services:
- `wpstime-punchclock.company` (secret = company/common id)
- `wpstime-punchclock` (account = username, secret = password)

### Option B: chat wizard setup (includes password; higher risk)
Only use if the user explicitly asks for chat-based setup and accepts that the password will appear in chat history/logs.

Workflow:
1) Warn clearly:
   - the password will be sent via chat and may be stored by the chat platform + gateway logs.
   - recommend Option A instead.
2) If they still confirm, collect 3 fields in separate turns:
   - companyId
   - username
   - password
3) Store into macOS Keychain on the SAME machine running the gateway using `security add-generic-password -U`:

```bash
security add-generic-password -U -s "wpstime-punchclock.company" -a "company" -w "<companyId>"
security add-generic-password -U -s "wpstime-punchclock" -a "<username>" -w "<password>"
```

4) Never echo the password back. After storing, run `status` to verify login works.

## Workflow
1) Run the punch script (headless by default):

```bash
node {baseDir}/scripts/punchclock.mjs --action <action>
```

Optional flags:
- `--headless 0` for debugging
- `--outDir <path>` to control screenshot output

2) Parse stdout JSON.
- On success: read `performed`, `screenshotPath`, and (optionally) pull key fields from `snippet`.
- On failure: report `error` and do not claim the punch succeeded.

3) Reply to the requesting channel with:
- one-line confirmation (what was performed)
- effective status/time if present (best-effort)
- attach the screenshot at `screenshotPath`

4) If the user asks to clock in/out but they may already be in that state, prefer running `status` first or immediately after to confirm and avoid double-punch confusion.

## Credentials (macOS Keychain)
Do not store secrets in files or prompts. Use Keychain.

Preferred services (used by `setup.mjs`):
- Service `wpstime-punchclock.company` → secret = company/common id
- Service `wpstime-punchclock` → account = username, secret = password

Backward-compat (older OpenClaw setups):
- `openclaw.wpstime.company`
- `openclaw.wpstime`

If missing, the punch script throws an error. When that happens, guide the user to run:

```bash
cd {baseDir}/scripts
node ./setup.mjs
```

Then retry the requested action.

## Reference
If you need the longer operational runbook, read:
- `references/PUNCHCLOCK_RUNBOOK.md`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
