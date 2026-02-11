# security-monitor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/chandrasekar-r/security-monitor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/chandrasekar-r/security-monitor/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Real-time security monitoring for Clawdbot. Detects intrusions, unusual API calls, credential usage patterns, and alerts on breaches.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Real-time security monitoring for Clawdbot. Detects intrusions, unusual API calls, credential usage patterns, and alerts on breaches.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run security-monitor`)
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
You are executing the security-monitor workflow. Use the following context:

Description: Real-time security monitoring for Clawdbot. Detects intrusions, unusual API calls, credential usage patterns, and alerts on breaches.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: security-monitor
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Security Monitor Skill

## When to use

Run continuous security monitoring to detect breaches, intrusions, and unusual activity on your Clawdbot deployment.

## Setup

No external dependencies required. Runs as a background process.

## How to

### Start real-time monitoring

```bash
node skills/security-monitor/scripts/monitor.cjs --interval 60
```

### Run in daemon mode (background)

```bash
node skills/security-monitor/scripts/monitor.cjs --daemon --interval 60
```

### Monitor for specific threats

```bash
node skills/security-monitor/scripts/monitor.cjs --threats=credentials,ports,api-calls
```

## What It Monitors

| Threat | Detection | Response |
|--------|-----------|----------|
| **Brute force attacks** | Failed login detection | Alert + IP tracking |
| **Port scanning** | Rapid connection attempts | Alert |
| **Process anomalies** | Unexpected processes | Alert |
| **File changes** | Unauthorized modifications | Alert |
| **Container health** | Docker issues | Alert |

## Output

- Console output (stdout)
- JSON logs at `/root/clawd/clawdbot-security/logs/alerts.log`
- Telegram alerts (configurable)

## Daemon Mode

Use systemd or PM2 to keep monitoring active:

```bash
# With PM2
pm2 start monitor.cjs --name "clawdbot-security" -- --daemon --interval 60
```

## Combined with Security Audit

Run audit first, then monitor continuously:

```bash
# One-time audit
node skills/security-audit/scripts/audit.cjs --full

# Continuous monitoring
node skills/security-monitor/scripts/monitor.cjs --daemon
```

## Related skills

- `security-audit` - One-time security scan (install separately)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
