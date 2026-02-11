# security-audit

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/chandrasekar-r/security-audit/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/chandrasekar-r/security-audit/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Comprehensive security auditing for Clawdbot deployments. Scans for exposed credentials, open ports, weak configs, and vulnerabilities. Auto-fix mode included.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Comprehensive security auditing for Clawdbot deployments. Scans for exposed credentials, open ports, weak configs, and vulnerabilities. Auto-fix mode included.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run security-audit`)
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
You are executing the security-audit workflow. Use the following context:

Description: Comprehensive security auditing for Clawdbot deployments. Scans for exposed credentials, open ports, weak configs, and vulnerabilities. Auto-fix mode included.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: security-audit
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Security Audit Skill

## When to use

Run a security audit to identify vulnerabilities in your Clawdbot setup before deployment or on a schedule. Use auto-fix to remediate common issues automatically.

## Setup

No external dependencies required. Uses native system tools where available.

## How to

### Quick audit (common issues)

```bash
node skills/security-audit/scripts/audit.cjs
```

### Full audit (comprehensive scan)

```bash
node skills/security-audit/scripts/audit.cjs --full
```

### Auto-fix common issues

```bash
node skills/security-audit/scripts/audit.cjs --fix
```

### Audit specific areas

```bash
node skills/security-audit/scripts/audit.cjs --credentials      # Check for exposed API keys
node skills/security-audit/scripts/audit.cjs --ports            # Scan for open ports
node skills/security-audit/scripts/audit.cjs --configs          # Validate configuration
node skills/security-audit/scripts/audit.cjs --permissions      # Check file permissions
node skills/security-audit/scripts/audit.cjs --docker           # Docker security checks
```

### Generate report

```bash
node skills/security-audit/scripts/audit.cjs --full --json > audit-report.json
```

## Output

The audit produces a report with:

| Level | Description |
|-------|-------------|
| 🔴 CRITICAL | Immediate action required (exposed credentials) |
| 🟠 HIGH | Significant risk, fix soon |
| 🟡 MEDIUM | Moderate concern |
| 🟢 INFO | FYI, no action needed |

## Checks Performed

### Credentials
- API keys in environment files
- Tokens in command history
- Hardcoded secrets in code
- Weak password patterns

### Ports
- Unexpected open ports
- Services exposed to internet
- Missing firewall rules

### Configs
- Missing rate limiting
- Disabled authentication
- Default credentials
- Open CORS policies

### Files
- World-readable files
- Executable by anyone
- Sensitive files in public dirs

### Docker
- Privileged containers
- Missing resource limits
- Root user in container

## Auto-Fix

The `--fix` option automatically:
- Sets restrictive file permissions (600 on .env)
- Secures sensitive configuration files
- Creates .gitignore if missing
- Enables basic security headers

## Related skills

- `security-monitor` - Real-time monitoring (available separately)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
