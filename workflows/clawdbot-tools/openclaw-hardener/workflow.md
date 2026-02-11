# openclaw-hardener

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/virtaava/openclaw-hardener/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/virtaava/openclaw-hardener/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Harden OpenClaw (workspace + ~/.openclaw): run openclaw security audit, catch prompt-injection/exfil risks, scan for secrets, and apply safe fixes (chmod/exec-bit cleanup). Includes optional config.patch planning to reduce attack surface.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Harden OpenClaw (workspace + ~/.openclaw): run openclaw security audit, catch prompt-injection/exfil risks, scan for secrets, and apply safe fixes (chmod/exec-bit cleanup). Includes optional config.patch planning to reduce attack surface.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run openclaw-hardener`)
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
You are executing the openclaw-hardener workflow. Use the following context:

Description: Harden OpenClaw (workspace + ~/.openclaw): run openclaw security audit, catch prompt-injection/exfil risks, scan for secrets, and apply safe fixes (chmod/exec-bit cleanup). Includes optional config.patch planning to reduce attack surface.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: openclaw-hardener
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# OpenClaw Hardener

This skill provides a **user-choice** hardening tool that can:

- Run OpenClaw’s built-in security audit (`openclaw security audit --deep` / `--fix`).
- Run workspace hygiene checks (exec bits, stray `.env`, unsafe serialization patterns, etc.).
- Apply safe mechanical fixes **only when explicitly requested**.
- Generate (and optionally apply) a **Gateway `config.patch` plan** to tighten runtime policy.

## Run the tool

Script:
- `skills_live/openclaw-hardener/scripts/hardener.py`

Examples:

```bash
# Read-only checks (recommended default)
python3 skills_live/openclaw-hardener/scripts/hardener.py check --all

# Only run OpenClaw built-in audit (deep)
python3 skills_live/openclaw-hardener/scripts/hardener.py check --openclaw

# Only run workspace checks
python3 skills_live/openclaw-hardener/scripts/hardener.py check --workspace

# Apply safe fixes (chmod/exec-bit cleanup + optionally openclaw audit --fix)
python3 skills_live/openclaw-hardener/scripts/hardener.py fix --all

# Generate a config.patch plan (prints JSON5 patch)
python3 skills_live/openclaw-hardener/scripts/hardener.py plan-config

# Apply the plan (requires a running gateway; uses `openclaw gateway call`)
python3 skills_live/openclaw-hardener/scripts/hardener.py apply-config
```

## Design rules (do not violate)

- **Default = check-only.** No file/config changes unless user runs `fix` or `apply-config`.
- **No secrets in output.** If a check reads sensitive paths, it must redact likely tokens.
- **Patch plans must be explicit.** Always show the patch before applying.

## What it checks / fixes

### OpenClaw built-in security audit
- Runs `openclaw security audit --deep` (and `--fix` in fix mode).

### Workspace hygiene (scope: workspace + ~/.openclaw)
- Permissions sanity under `~/.openclaw` (basic checks).
- Unexpected executable bits in non-executable filetypes.
- Stray `.env` files (warn) and tracked `.env` (fail).
- Risky deserialization / unsafe patterns in our scripts (heuristics).

### Config hardening (optional plan)
Generates a conservative `config.patch` template focusing on:
- Tightening inbound access defaults (pairing/allowlist, mention gating) **only if you opt-in**.
- Ensuring sensitive log redaction is enabled.

(Exact keys depend on your config; the plan is best-effort and should be reviewed.)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
