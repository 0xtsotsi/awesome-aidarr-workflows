# skill-scanner

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/bvinci1-design/skill-scanner/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/bvinci1-design/skill-scanner/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Scan Clawdbot and MCP skills for malware, spyware, crypto-miners, and malicious code patterns before you install them. Security audit tool that detects data exfiltration, system modification attempts, backdoors, and obfuscation techniques.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Scan Clawdbot and MCP skills for malware, spyware, crypto-miners, and malicious code patterns before you install them. Security audit tool that detects data exfiltration, system modification attempts, backdoors, and obfuscation techniques.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run skill-scanner`)
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
You are executing the skill-scanner workflow. Use the following context:

Description: Scan Clawdbot and MCP skills for malware, spyware, crypto-miners, and malicious code patterns before you install them. Security audit tool that detects data exfiltration, system modification attempts, backdoors, and obfuscation techniques.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: skill-scanner
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Skill Scanner

Security audit tool for Clawdbot/MCP skills - scans for malware, spyware, crypto-mining, and malicious patterns.

## Capabilities
- Scan skill folders for security threats
- Detect data exfiltration patterns
- Identify system modification attempts
- Catch crypto-mining indicators
- Flag arbitrary code execution risks
- Find backdoors and obfuscation techniques
- Output reports in Markdown or JSON format
- Provide Web UI via Streamlit

## Usage

### Command Line
```bash
python skill_scanner.py /path/to/skill-folder
```

### Within Clawdbot
```
"Scan the [skill-name] skill for security issues using skill-scanner"
"Use skill-scanner to check the youtube-watcher skill"
"Run a security audit on the remotion skill"
```

### Web UI
```bash
pip install streamlit
streamlit run streamlit_ui.py
```

## Requirements
- Python 3.7+
- No additional dependencies (uses Python standard library)
- Streamlit (optional, for Web UI)

## Entry Point
- **CLI:** `skill_scanner.py`
- **Web UI:** `streamlit_ui.py`

## Tags
#security #malware #spyware #crypto-mining #scanner #audit #code-analysis #mcp #clawdbot #agent-skills #safety #threat-detection #vulnerability

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
