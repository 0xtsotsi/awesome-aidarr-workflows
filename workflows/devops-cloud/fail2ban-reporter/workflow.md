# fail2ban-reporter

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jestersimpps/fail2ban-reporter/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jestersimpps/fail2ban-reporter/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Auto-report fail2ban banned IPs to AbuseIPDB and notify via Telegram. Use when monitoring server security, reporting attackers, or checking banned IPs. Watches fail2ban for new bans, reports them to AbuseIPDB, and sends alerts.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Auto-report fail2ban banned IPs to AbuseIPDB and notify via Telegram. Use when monitoring server security, reporting attackers, or checking banned IPs. Watches fail2ban for new bans, reports them to AbuseIPDB, and sends alerts.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run fail2ban-reporter`)
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
You are executing the fail2ban-reporter workflow. Use the following context:

Description: Auto-report fail2ban banned IPs to AbuseIPDB and notify via Telegram. Use when monitoring server security, reporting attackers, or checking banned IPs. Watches fail2ban for new bans, reports them to AbuseIPDB, and sends alerts.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: fail2ban-reporter
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# fail2ban Reporter

Monitor fail2ban bans and auto-report attackers to AbuseIPDB.

## Setup

1. Get a free AbuseIPDB API key at https://www.abuseipdb.com/account/api
2. Store it: `pass insert abuseipdb/api-key`
3. Install the monitor: `bash {baseDir}/scripts/install.sh`

## Manual Usage

### Report all currently banned IPs

```bash
bash {baseDir}/scripts/report-banned.sh
```

### Check a specific IP

```bash
bash {baseDir}/scripts/check-ip.sh <ip>
```

### Show ban stats

```bash
bash {baseDir}/scripts/stats.sh
```

## Auto-Reporting

The install script sets up a fail2ban action that auto-reports new bans.

```bash
bash {baseDir}/scripts/install.sh    # install auto-reporting
bash {baseDir}/scripts/uninstall.sh  # remove auto-reporting
```

## Heartbeat Integration

Add to HEARTBEAT.md to check for new bans periodically:

```markdown
- [ ] Check fail2ban stats and report any unreported IPs to AbuseIPDB
```

## Workflow

1. fail2ban bans an IP → action triggers `report-single.sh`
2. Script reports to AbuseIPDB with SSH brute-force category
3. Sends Telegram notification (if configured)
4. Logs report to `/var/log/abuseipdb-reports.log`

## API Reference

See [references/abuseipdb-api.md](references/abuseipdb-api.md) for full API docs.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
