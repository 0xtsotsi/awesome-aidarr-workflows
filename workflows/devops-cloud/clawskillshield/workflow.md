# clawskillshield

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/abyousef739/clawskillshield/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/abyousef739/clawskillshield/SKILL.md)
> Category: DevOps & Cloud

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
**Trigger:** User-invocable (via `aidarr run clawskillshield`)
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
You are executing the clawskillshield workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: clawskillshield
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# ClawSkillShield 🛡️

**Local-first security scanner for OpenClaw/ClawHub skills.**

## What It Does

- **Static analysis** for security risks and malware patterns
- **Detects**:
  - Hardcoded secrets (API keys, credentials, private keys)
  - Risky imports (`os`, `subprocess`, `socket`, `ctypes`)
  - Dangerous calls (`eval()`, `exec()`, `open()`)
  - Obfuscation (base64 blobs, suspicious encoding)
  - Hardcoded IPs
- **Risk scoring** (0–10) + detailed threat reports
- **Quarantine** high-risk skills automatically

## Dual-Use Design

- **CLI for humans**: Quick safety checks before installing skills
- **Agent API**: Importable functions for autonomous agents/Moltbots to proactively scan and quarantine risky skills (essential post-ClawHavoc)

## Quick Start

### CLI (Humans)
```bash
pip install -e .
clawskillshield scan-local /path/to/skill
clawskillshield quarantine /path/to/skill
```

### Python API (Agents)
```python
from clawskillshield import scan_local, quarantine

threats = scan_local("/path/to/skill")
if risk_score < 4:  # HIGH RISK
    quarantine("/path/to/skill")
```

## Zero Dependencies
Pure Python. No network calls. Runs entirely locally.

## Why This Matters
ClawHavoc demonstrated how easily malicious skills can slip into the ecosystem. ClawSkillShield provides a trusted, open-source defense layer—audit the code, run offline, stay safe.

---

**GitHub**: https://github.com/AbYousef739/clawskillshield  
**License**: MIT  
**Author**: Ab Yousef  
**Contact**: contact@clawskillshield.com

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
