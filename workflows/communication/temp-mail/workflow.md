# temp-mail

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/techwithanirudh/temp-mail/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/techwithanirudh/temp-mail/SKILL.md)
> Category: Communication

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
**Trigger:** User-invocable (via `aidarr run temp-mail`)
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
You are executing the temp-mail workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: temp-mail
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# temp-mail skill

This skill provides a Python CLI script to interact with the hosted Vortex API (GET /emails/{email}, DELETE /emails/{email}/clear).

Usage examples (scripts are in scripts/):

- create: generates a random localpart and prints an address for the provided domain
- fetch: queries the Vortex HTTP API to list messages for an address
- poll: wait until messages arrive or timeout
- clear: delete all messages for an address

Run with uv: `uv run {baseDir}/scripts/temp_mail.py` (script includes shebang and metadata header similar to the hn skill)

Examples:

```bash
# generate a random address
uv run {baseDir}/scripts/temp_mail.py create

# fetch messages for an address
uv run {baseDir}/scripts/temp_mail.py fetch alice@dash.dino.icu

# poll until messages arrive (timeout 60s)
uv run {baseDir}/scripts/temp_mail.py poll alice@dash.dino.icu --timeout 60

# clear mailbox
uv run {baseDir}/scripts/temp_mail.py clear alice@dash.dino.icu
```

Defaults:
- VORTEX_URL: https://vtx-api.skyfall.dev
- default domain: skyfall.dev (override with VORTEX_DOMAIN env var)

Install

```bash
# create a venv and install deps (unix)
python -m venv .venv
source .venv/bin/activate
python -m pip install --upgrade pip
python -m pip install -r scripts/requirements.txt

# or using uv which creates an ephemeral venv for you, e.g.
uv run {baseDir}/scripts/temp_mail.py create
```

Notes:
- script uses httpx for requests; rich is optional and omitted from requirements
- random username generation mirrors the frontend behavior (lowercase alphanumeric), attempted to replicate falso randUserName behavior
- hosted instance includes multiple domains, e.g., dash.dino.icu, skyfall.dev, etc. When creating addresses, choose a domain from that list or let the script use the default


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
