# moltiumv2-lite

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/cariciman/moltiumv2-lite/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/cariciman/moltiumv2-lite/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Lightweight Clawhub bootstrap skill for MoltiumV2. Downloads the full RPC-first local toolkit from https://moltium.fun and runs init/doctor.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Lightweight Clawhub bootstrap skill for MoltiumV2. Downloads the full RPC-first local toolkit from https://moltium.fun and runs init/doctor.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run moltiumv2-lite`)
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
You are executing the moltiumv2-lite workflow. Use the following context:

Description: Lightweight Clawhub bootstrap skill for MoltiumV2. Downloads the full RPC-first local toolkit from https://moltium.fun and runs init/doctor.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: moltiumv2-lite
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# MoltiumV2 (Clawhub Lite Bootstrap)

This Clawhub upload is intentionally **small** (text-only) to avoid upload limits.
It bootstraps the full MoltiumV2 toolkit from the canonical website:

- Index / docs: https://moltium.fun/skill.md
- Skillpack artifacts:
  - https://moltium.fun/MoltiumV2-skillpack-latest.zip
  - https://moltium.fun/MoltiumV2-skillpack-latest.tar.gz

## Quick start

From the folder where you installed/uploaded this Clawhub skill, run:

```bash
node scripts/bootstrap.mjs
```

Optional environment variables:
- `MOLTIUMV2_DIR` — install target folder (default: `MoltiumV2`)
- `MOLTIUMV2_BASE_URL` — override download base (default: `https://moltium.fun`)

What it does:
- downloads `MoltiumV2-skillpack-latest.tar.gz`
- extracts to `MOLTIUMV2_DIR`
- runs `npm install`
- runs `ctl.mjs init --pretty` (auto-generates wallet if missing)
- runs `ctl.mjs doctor --pretty`

Then fund the printed wallet pubkey before sending real transactions.

## Safety rules (must)

- Never paste seed phrases into chats.
- Start with `--simulate` before real trades.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
