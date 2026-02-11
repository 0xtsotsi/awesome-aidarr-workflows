# senseguard

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/fermionoid/senseguard/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/fermionoid/senseguard/SKILL.md)
> Category: AI & LLMs

---

## Description

Semantic security scanner for OpenClaw skills. Detects prompt injection, data exfiltration, and hidden instructions that traditional code scanners miss. Use when user asks to scan skills, check skill safety, or run a security audit.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Semantic security scanner for OpenClaw skills. Detects prompt injection, data exfiltration, and hidden instructions that traditional code scanners miss. Use when user asks to scan skills, check skill safety, or run a security audit.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run senseguard`)
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
You are executing the senseguard workflow. Use the following context:

Description: Semantic security scanner for OpenClaw skills. Detects prompt injection, data exfiltration, and hidden instructions that traditional code scanners miss. Use when user asks to scan skills, check skill safety, or run a security audit.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: senseguard
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# SenseGuard

Scans OpenClaw skills for **natural language security threats** — the kind that VirusTotal and traditional code scanners cannot detect.

Traditional scanners see SKILL.md as a text file. SenseGuard sees it as **agent instructions** and checks for prompt injection, data exfiltration, obfuscation, and persistence attacks.

## How to Use

When the user asks to scan a skill:

```bash
python3 scripts/scanner.py --target <skill-name-or-path>
```

Options:
- `--target all` — scan all installed skills
- `--deep` — force LLM semantic analysis (Layer 2)
- `--no-cache` — skip cached results
- `--json` — output raw JSON for further processing

### Layer 2 (Semantic Analysis)

When `--json` output contains a `layer2_prompt` field, process it as a security audit task, then feed the JSON result back to generate the final score. This is how the LLM analyzes intent beyond regex patterns.

## Output

The scanner outputs a Markdown risk report with:
- Score (0-100) and rating: SAFE / CAUTION / DANGEROUS / MALICIOUS
- Findings with rule IDs, evidence text, and line numbers
- Actionable recommendations

For CRITICAL findings, clearly advise the user to take action.

## Key Differentiator

SenseGuard catches what VirusTotal cannot:
- `"ignore all previous instructions"` — prompt injection
- `curl -X POST` hidden in Markdown — data exfiltration
- Zero-width characters hiding commands — obfuscation
- `"modify MEMORY.md"` — persistence attacks

These are invisible to traditional malware scanners because they target the **AI agent**, not the operating system.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
