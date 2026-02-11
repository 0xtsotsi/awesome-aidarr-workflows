# sona-security-audit

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/virtaava/sona-security-audit/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/virtaava/sona-security-audit/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Fail-closed security auditing for OpenClaw/ClawHub skills & repos: trufflehog secrets scanning, semgrep SAST, prompt-injection/persistence signals, and supply-chain hygiene checks before enabling or installing.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Fail-closed security auditing for OpenClaw/ClawHub skills & repos: trufflehog secrets scanning, semgrep SAST, prompt-injection/persistence signals, and supply-chain hygiene checks before enabling or installing.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run sona-security-audit`)
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
You are executing the sona-security-audit workflow. Use the following context:

Description: Fail-closed security auditing for OpenClaw/ClawHub skills & repos: trufflehog secrets scanning, semgrep SAST, prompt-injection/persistence signals, and supply-chain hygiene checks before enabling or installing.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: sona-security-audit
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# security-audit

A hostile-by-design, **fail-closed** audit workflow for codebases and OpenClaw/ClawHub skills.

It does **not** try to answer “does this skill work?”.
It tries to answer: **“can this skill betray the system?”**

## What it checks (high level)

This skill’s scripts combine multiple layers:

- **Secrets / credential leakage:** trufflehog
- **Static analysis:** semgrep (auto rules)
- **Hostile repo audit (custom):** prompt-injection signals, persistence mechanisms, suspicious artifacts, dependency hygiene

If any layer fails, the overall audit is **FAIL**.

## Run an audit (JSON)

From this skill folder (use `bash` so it works even if executable bits were not preserved by a zip download):

```bash
bash scripts/run_audit_json.sh <path>
```

Example:

```bash
bash scripts/run_audit_json.sh . > /tmp/audit.json
jq '.ok, .tools' /tmp/audit.json
```

### Security levels (user configurable)

Set the strictness level (default: `standard`):

```bash
OPENCLAW_AUDIT_LEVEL=standard bash scripts/run_audit_json.sh <path>
OPENCLAW_AUDIT_LEVEL=strict   bash scripts/run_audit_json.sh <path>
OPENCLAW_AUDIT_LEVEL=paranoid bash scripts/run_audit_json.sh <path>
```

- `standard`: pragmatic strict defaults (lockfiles required; install hooks/persistence/prompt-injection signals fail)
- `strict`: more patterns become hard FAIL (e.g. minified/obfuscation artifacts)
- `paranoid`: no "best-effort" hashing failures; more fail-closed behavior

## Manifest requirement (for zero-trust install workflows)

For strict/quarantine workflows, require a machine-readable intent/permissions manifest at repo root:

- `openclaw-skill.json`

If a repo/skill does not provide this manifest, the hostile audit should treat it as **FAIL**.

See: `docs/OPENCLAW_SKILL_MANIFEST_SCHEMA.md`.

## Optional: execution sandbox (Docker)

Docker is **optional** here. This skill can be used for static auditing without Docker.

If you want to execute any generated/untrusted code, run it in a separate sandbox workflow (recommended).

## Files

- `scripts/run_audit_json.sh` — main JSON audit runner
- `scripts/hostile_audit.py` — prompt-injection/persistence/dependency hygiene scanner
- `scripts/security_audit.sh` — convenience wrapper (always returns JSON, never non-zero)
- `openclaw-skill.json` — machine-readable intent/permissions manifest

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
