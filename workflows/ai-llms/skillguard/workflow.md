# skillguard

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/c-goro/skillguard/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/c-goro/skillguard/SKILL.md)
> Category: AI & LLMs

---

## Description

Security scanner for AgentSkill packages. Scan skills for credential theft, code injection, prompt manipulation, data exfiltration, and evasion techniques before installing them. Use when evaluating skills from ClawHub or any untrusted source.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Security scanner for AgentSkill packages. Scan skills for credential theft, code injection, prompt manipulation, data exfiltration, and evasion techniques before installing them. Use when evaluating skills from ClawHub or any untrusted source.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run skillguard`)
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
You are executing the skillguard workflow. Use the following context:

Description: Security scanner for AgentSkill packages. Scan skills for credential theft, code injection, prompt manipulation, data exfiltration, and evasion techniques before installing them. Use when evaluating skills from ClawHub or any untrusted source.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: skillguard
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# SkillGuard — Agent Security Scanner

When asked to check, audit, or scan a skill for security, use SkillGuard.

## Commands

### Scan a local skill directory
```bash
node /home/claw/.openclaw/workspace/skillguard/src/cli.js scan <path>
```

### Scan with compact output (for chat)
```bash
node /home/claw/.openclaw/workspace/skillguard/src/cli.js scan <path> --compact
```

### Check text for prompt injection
```bash
node /home/claw/.openclaw/workspace/skillguard/src/cli.js check "<text>"
```

### Batch scan multiple skills
```bash
node /home/claw/.openclaw/workspace/skillguard/src/cli.js batch <directory>
```

### Scan a ClawHub skill by slug
```bash
node /home/claw/.openclaw/workspace/skillguard/src/cli.js scan-hub <slug>
```

## Score Interpretation
- 80-100 ✅ LOW risk — safe to install
- 50-79 ⚠️ MEDIUM — review findings before installing
- 20-49 🟠 HIGH — significant security concerns
- 0-19 🔴 CRITICAL — do NOT install without manual review

## Output Formats
- Default: full text report
- `--compact`: chat-friendly summary
- `--json`: machine-readable full report
- `--quiet`: score and verdict only

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
