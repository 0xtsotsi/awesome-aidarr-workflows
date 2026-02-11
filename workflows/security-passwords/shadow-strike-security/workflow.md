# shadow-strike-security

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/malvex007/shadow-strike-security/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/malvex007/shadow-strike-security/SKILL.md)
> Category: Security & Passwords

---

## Description

Elite penetration testing platform with 600+ security tools

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Elite penetration testing platform with 600+ security tools

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run shadow-strike-security`)
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
You are executing the shadow-strike-security workflow. Use the following context:

Description: Elite penetration testing platform with 600+ security tools

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: shadow-strike-security
category: Security & Passwords
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# ShadowStrike Security

**Elite Penetration Testing & Security Assessment Platform**

Transform OpenClaw into a professional security operations center with 600+ Kali Linux tools, intelligent orchestration, and automated reporting.

## What is ShadowStrike?

ShadowStrike is a comprehensive security testing platform that provides:
- **Intelligent Tool Orchestration** - Auto-selects best tools for each task
- **Complete PT Lifecycle** - From reconnaissance to professional reporting
- **600+ Security Tools** - Full Kali Linux arsenal at your fingertips
- **Automated Workflows** - One command executes entire assessments

## Key Features

### 🎯 Intelligent Reconnaissance
- **Network Discovery:** nmap, masscan, unicornscan
- **Web Enumeration:** dirb, gobuster, ffuf, wfuzz
- **Subdomain Hunting:** amass, sublist3r, assetfinder
- **OSINT Gathering:** theHarvester, recon-ng, maltego

### 🔍 Vulnerability Assessment
- **Web Testing:** sqlmap, nikto, dalfox, nuclei
- **Network Scanning:** 610+ NSE scripts
- **SSL/TLS Analysis:** testssl.sh, sslscan, sslyze
- **Configuration Review:** Automated misconfiguration detection

### ⚔️ Professional Exploitation
- **Web Exploits:** SQL injection, XSS, LFI, RCE testing
- **Password Attacks:** hashcat, john, hydra (GPU-accelerated)
- **Wireless Auditing:** aircrack-ng, wifite, reaver
- **Frameworks:** Metasploit, searchsploit, BeEF

### 🛡️ Post-Exploitation
- **Privilege Escalation:** linpeas, winpeas
- **Lateral Movement:** Pivoting and tunneling
- **Persistence Testing:** Backdoor detection
- **Data Exfiltration:** Secure transfer methods

### 📊 Professional Reporting
- **Executive Summaries:** High-level risk overview
- **Technical Reports:** CVE correlation, PoC details
- **Remediation Guides:** Step-by-step fixes
- **Evidence Collection:** Screenshots and logs

## Quick Start

### Installation
```bash
cp -r shadowstrike-security ~/.openclaw/skills/
```

Add to agent config:
```json
{
  "skills": ["shadowstrike-security"]
}
```

Restart:
```bash
pkill -f "openclaw gateway" && openclaw gateway &
```

### First Commands
```
"scan target.com"          → Quick port scan
"web target.com"           → Web application test
"pentest target.com"       → Full penetration test
"wifi"                     → WiFi security audit
"hashes crack hash.txt"    → Password cracking
```

## Command Reference

### Network Assessment

| Command | Description | Example Output |
|---------|-------------|----------------|
| `scan [target]` | Quick port scan | `Ports: 22,80,443` |
| `deep [target]` | Full port scan (all 65,535) | `[Complete scan]` |
| `services [target]` | Service detection | `80:nginx, 3306:mysql` |
| `os [target]` | OS fingerprinting | `Linux 5.4` |

### Web Application Testing

| Command | Description | Example Output |
|---------|-------------|----------------|
| `web [target]` | Full web app test | `SQLi found, XSS medium` |
| `dirb [target]` | Directory discovery | `/admin, /api, /config` |
| `sql [target]` | SQL injection test | `Vulnerable: id parameter` |
| `xss [target]` | XSS testing | `Reflected XSS confirmed` |
| `vuln [target]` | Vulnerability scan | `Critical: 2, High: 5` |

### Complete Workflows

| Command | Description | Duration |
|---------|-------------|----------|
| `pentest [target]` | Full PT lifecycle | 10-30 min |
| `bugbounty [target]` | Bug bounty hunting | 15-45 min |
| `audit [network]` | Network security audit | 20-60 min |
| `compliance [target]` | Compliance check | 30-90 min |

### Specialized Tools

| Command | Description |
|---------|-------------|
| `wifi` | WiFi security audit |
| `hashes [file]` | Crack password hashes |
| `exploit [cve]` | Search and run exploits |
| `report` | Generate security report |

## How It Works

### Intelligent Tool Selection

ShadowStrike automatically chooses the best tools:

**For Web Targets:**
```
Input: "test web target.com"
ShadowStrike:
  1. whatweb → Technology fingerprinting
  2. dirb → Directory discovery
  3. nikto → Vulnerability scanning
  4. sqlmap → SQL injection test
  5. dalfox → XSS testing
  6. nuclei → CVE scanning
Output: "Critical: 2, High: 5, Report: ./target-security.md"
```

**For Network Targets:**
```
Input: "scan 192.168.1.0/24"
ShadowStrike:
  1. nmap -sS → Port scanning
  2. nmap -sV → Service detection
  3. nmap -O → OS fingerprinting
  4. nmap --script=vulners → Vuln detection
Output: "Hosts: 15, Open ports: 47, Vulnerabilities: 12"
```

## Tool Arsenal

### Information Gathering (50+ tools)
```
nmap, masscan, unicornscan, zmap
theHarvester, recon-ng, maltego
amass, sublist3r, assetfinder, findomain
```

### Web Testing (60+ tools)
```
nikto, sqlmap, burpsuite, zap
dirb, gobuster, wfuzz, ffuf
dalfox, xsser, nuclei, arachni
wpscan, joomscan, droopescan
```

### Password Attacks (30+ tools)
```
hashcat (GPU-accelerated), john, hydra
medusa, ncrack, patator, crowbar
crunch, cewl, cupp (wordlist generators)
```

### Wireless (25+ tools)
```
aircrack-ng, wifite, reaver, bully
kismet, wireshark, airmon-ng
hostapd-wpe, freeradius-wpe
```

### Exploitation (35+ tools)
```
metasploit, searchsploit, beef
setoolkit, sqlmap, commix
routersploit, exploitdb
```

### Forensics (40+ tools)
```
autopsy, sleuthkit, volatility
foremost, scalpel, binwalk
yara, cuckoo, remnux, ghidra
```

## Workflow Examples

### Example 1: Bug Bounty Hunting

```
You: "bugbounty target.com"

ShadowStrike executes:
✓ Subdomain enumeration (amass, sublist3r)
✓ Screenshot all services
✓ Technology fingerprinting
✓ Vulnerability scanning (nikto, nuclei)
✓ SQL injection testing (sqlmap)
✓ XSS testing (dalfox, xsser)
✓ SSL/TLS analysis (testssl.sh)

Results:
💰 Critical (P1): 1 - SQL Injection
💰 High (P2): 3 - XSS, IDOR, LFI
💰 Medium (P3): 5 - Various issues

Reports:
📄 P1-SQLi-report.md (Ready to submit)
📄 P2-XSS-report.md (Ready to submit)
📄 P2-IDOR-report.md (Ready to submit)

Potential Bounty: $2,000 - $5,000
```

### Example 2: Network Security Audit

```
You: "audit 192.168.1.0/24"

ShadowStrike executes:
✓ Host discovery (nmap -sn)
✓ Port scanning (nmap -sS -p-)
✓ Service detection (nmap -sV)
✓ OS fingerprinting (nmap -O)
✓ Vulnerability scanning (nmap --script=vulners)
✓ SSL testing (testssl.sh)
✓ Default credential testing

Results:
Hosts Found: 23
Open Ports: 147
Services: 89
Vulnerabilities: 34 (Critical: 3, High: 8, Medium: 23)

Report: ./network-audit-report.md
```

### Example 3: Full Penetration Test

```
You: "pentest target.com"

Phase 1: Reconnaissance (5 min)
✓ Subdomain enumeration
✓ IP range discovery
✓ Technology stack identification
✓ DNS enumeration

Phase 2: Scanning (10 min)
✓ Port scanning
✓ Service detection
✓ OS fingerprinting

Phase 3: Enumeration (10 min)
✓ User enumeration
✓ Share discovery
✓ Directory brute-forcing

Phase 4: Vulnerability Assessment (15 min)
✓ Automated scanning
✓ Manual verification
✓ Exploit research

Phase 5: Exploitation (10 min)
✓ Attempt exploitation
✓ Proof of concept
✓ Credential testing

Phase 6: Post-Exploitation (10 min)
✓ Privilege escalation testing
✓ Lateral movement
✓ Data collection

Phase 7: Reporting (5 min)
✓ Executive summary
✓ Technical findings
✓ Risk ratings
✓ Remediation steps

Final Report:
Security Score: 68/100
Critical: 2, High: 5, Medium: 8, Low: 12

Full Report: ./pentest-target-report.md
Remediation: ./pentest-target-remediation.md
Evidence: ./pentest-target-evidence/
```

## Legal & Ethics

**⚠️ IMPORTANT: Use Responsibly**

**You CAN:**
- ✅ Test systems you own
- ✅ Test systems with written authorization
- ✅ Conduct authorized penetration tests
- ✅ Perform security audits on your infrastructure
- ✅ Participate in bug bounty programs (within scope)

**You CANNOT:**
- ❌ Test systems without permission
- ❌ Attack systems illegally
- ❌ Violate privacy laws
- ❌ Cause damage to systems
- ❌ Steal data

**Legal Notice:**
Unauthorized access is illegal under:
- Computer Fraud and Abuse Act (CFAA)
- Computer Misuse Act (UK)
- Similar laws worldwide

Always obtain proper authorization before testing.

## Requirements

- OpenClaw >= 2026.2.3
- Kali Linux 2024.x (recommended)
- Sudo access for privileged operations
- 4GB RAM minimum (8GB recommended)
- 20GB free disk space

## License

MIT License - Free for educational and authorized security testing

---

**ShadowStrike Security: Professional Tools for Professional Testing** ⚔️🛡️

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
