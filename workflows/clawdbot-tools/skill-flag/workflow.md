# skill-flag

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/patfire94/skill-flag/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/patfire94/skill-flag/SKILL.md)
> Category: Clawdbot Tools

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
**Trigger:** User-invocable (via `aidarr run skill-flag`)
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
You are executing the skill-flag workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: skill-flag
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Skill Flag Skill 🛡️

Scan Clawdbot/OpenClaw skills for malicious patterns, backdoors, and security risks.

**Created by:** DarkM00n (Bug Bounty Hunter & Security Researcher)

## Commands

### Scan All Installed Skills
```
scan skills
scan all skills
security scan
```

### Scan Specific Skill
```
scan skill <skill-name>
check skill <skill-name>
```

### Scan Before Installing (URL/Path)
```
scan skill url <clawdhub-url>
pre-scan <skill-name>
```

### Quick Risk Report
```
skill risk report
security report
```

## How To Use

Run the scanner:
```bash
python3 skills/skill-flag/scanner.py [--skill NAME] [--all] [--verbose]
```

Or ask the agent:
- "Scan all my installed skills for security issues"
- "Check if the crypto-tracker skill is safe"
- "Give me a security report"

## What It Detects

| Category | Risk Level | Examples |
|----------|------------|----------|
| 🔴 Data Exfiltration | CRITICAL | curl/wget to external domains, fetch(), requests.post() |
| 🔴 Backdoors | CRITICAL | Reverse shells, nc -e, bash -i, encoded payloads |
| 🔴 Credential Theft | CRITICAL | Access to ~/.ssh, ~/.aws, API keys, .env files |
| 🟠 Prompt Injection | HIGH | "ignore previous", "system override", "new instructions" |
| 🟠 Code Execution | HIGH | eval(), exec(), subprocess with shell=True |
| 🟡 Persistence | MEDIUM | Cron jobs, systemd units, startup scripts |
| 🟡 Obfuscation | MEDIUM | Base64 encoded commands, hex strings, rot13 |
| 🟢 Suspicious | LOW | Uncommon imports, network activity |

## Risk Score

Each skill gets a score from 0-100:
- **0-20**: ✅ Clean - No issues found
- **21-40**: 🟢 Low Risk - Minor concerns
- **41-60**: 🟡 Medium Risk - Review recommended  
- **61-80**: 🟠 High Risk - Careful inspection needed
- **81-100**: 🔴 Critical - Do not use without audit

## Output

Reports saved to: `skills/skill-flag/reports/`

Example output:
```
🛡️ SECURITY SCAN REPORT
━━━━━━━━━━━━━━━━━━━━━━━
Scanned: 12 skills
Clean: 9
Warnings: 2
Critical: 1

⚠️ WARNINGS:
- crypto-tracker: External API calls (expected for price data)
- web-scraper: Uses requests library

🔴 CRITICAL:
- shady-skill: 
  - Line 45: curl to unknown domain
  - Line 67: Base64 encoded payload
  - Line 89: Reads ~/.ssh/id_rsa
  RECOMMENDATION: Remove immediately
```

## Directories Scanned

1. `~/.clawdbot/skills/` - Global installed skills
2. `./skills/` - Workspace skills
3. `~/.npm-global/lib/node_modules/clawdbot/skills/` - Built-in skills

## False Positives

Some legitimate skills need network access or file operations. The scanner flags them for review but doesn't auto-block. Use judgment:
- Price trackers → API calls expected ✓
- Email skills → Network access expected ✓
- File managers → File operations expected ✓

## Pro Version (Coming Soon)

- Continuous monitoring
- ClawdHub pre-install scanning
- Custom whitelist/blacklist
- Scheduled reports
- Webhook alerts

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
