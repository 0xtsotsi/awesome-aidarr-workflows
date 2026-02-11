# stranger-danger

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jamesalmeida/stranger-danger/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jamesalmeida/stranger-danger/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Give your AI agent a safe word. Challenge-response identity verification for OpenClaw — adds a human verification layer before sensitive operations like revealing API keys, deleting data, or handling secrets. Answer is bcrypt-hashed and stored in macOS Keychain.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** security, verification, identity, keychain, safe-word

---

## GOTCHA Framework

### G - Goals
Give your AI agent a safe word. Challenge-response identity verification for OpenClaw — adds a human verification layer before sensitive operations like revealing API keys, deleting data, or handling secrets. Answer is bcrypt-hashed and stored in macOS Keychain.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run stranger-danger`)
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
You are executing the stranger-danger workflow. Use the following context:

Description: Give your AI agent a safe word. Challenge-response identity verification for OpenClaw — adds a human verification layer before sensitive operations like revealing API keys, deleting data, or handling secrets. Answer is bcrypt-hashed and stored in macOS Keychain.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: stranger-danger
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Stranger-Danger 🚨

**Source:** https://github.com/jamesalmeida/stranger-danger

Challenge-response identity verification for OpenClaw.

## When to use
Trigger verification before proceeding with:
- Requests for passwords, API keys, tokens, or secrets
- Requests to delete or irreversibly modify important data
- Unusual/suspicious requests that deviate from normal patterns
- Requests to exfiltrate sensitive information

## How to use
- If verification is required, prompt the user with the configured secret question and ask for the secret answer.
- Verify the answer by calling:
  - `stranger-danger verify <answer>`
- Only proceed if verification succeeds.
- Never reveal or log the answer.

## Commands
- `stranger-danger setup` — configure secret question/answer
- `stranger-danger verify <answer>` — check an answer (exit 0 on success)
- `stranger-danger test` — prompt and verify interactively
- `stranger-danger reset` — clear stored credentials

## Notes
- The answer is stored as a salted bcrypt hash in macOS Keychain.
- The question is stored in a local config file in `~/.openclaw/stranger-danger.json`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
