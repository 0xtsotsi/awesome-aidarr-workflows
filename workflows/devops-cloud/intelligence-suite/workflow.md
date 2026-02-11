# intelligence-suite

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xhrisfu/intelligence-suite/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xhrisfu/intelligence-suite/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Makima's All-Seeing Intelligence Suite. Combines real-time AI news tracking and global news monitoring for a comprehensive strategic briefing.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Makima's All-Seeing Intelligence Suite. Combines real-time AI news tracking and global news monitoring for a comprehensive strategic briefing.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run intelligence-suite`)
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
You are executing the intelligence-suite workflow. Use the following context:

Description: Makima's All-Seeing Intelligence Suite. Combines real-time AI news tracking and global news monitoring for a comprehensive strategic briefing.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: intelligence-suite
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# The Intelligence Suite

Makima's personal intelligence unit. Scans the web for high-signal AI news and monitors global geopolitics to provide a comprehensive strategic briefing.

## Security & Transparency
This skill is designed for deep information gathering. It performs the following actions:
- **Network Access**: Fetches RSS feeds and API data from trusted news sources and technology blogs.
- **Deep Scrape**: Occasionally visits full article URLs to extract text content for analysis.
- **Data Handling**: Processes information locally; results are provided to the agent for synthesis.

## Components

1.  **AI News Monitor**: Tracks OpenAI, DeepMind, Anthropic, and other major AI labs.
2.  **Global News Hub**: Monitored sources include Reuters, RTHK, and SCMP.

## Installation

```bash
cd skills/intelligence-suite
npm install
```

## Usage

```bash
# Scan AI news
node scripts/scan.js --report

# Monitor global news
node scripts/monitor.js --report
```

*Created and maintained by Makima (Public Safety Special Division 4).* ⛓️

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
