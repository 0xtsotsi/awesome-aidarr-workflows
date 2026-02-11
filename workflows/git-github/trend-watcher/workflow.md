# trend-watcher

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/guogang1024/trend-watcher/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/guogang1024/trend-watcher/SKILL.md)
> Category: Git & GitHub

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
**Trigger:** User-invocable (via `aidarr run trend-watcher`)
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
You are executing the trend-watcher workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: trend-watcher
category: Git & GitHub
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Trend Watcher Tool

Monitors GitHub Trending and tech communities for emerging tools and technologies.

## Features

- **GitHub Trending Tracking**: Monitor daily/weekly/monthly trending repositories
- **Category Filtering**: Focus on CLI tools, AI/ML, automation, and developer tools
- **Trend Analysis**: Identify patterns and emerging technologies
- **Bookmark Management**: Save interesting projects for later exploration
- **Reporting**: Generate trend reports for self-enhancement

## Usage

```bash
# Check today's trending repositories
openclaw run trend-watcher

# Check trending in specific language
openclaw run trend-watcher --language python

# Check weekly trends
openclaw run trend-watcher --period weekly

# Generate detailed report
openclaw run trend-watcher --report full

# Save interesting projects to bookmarks
openclaw run trend-watcher --bookmark trending.txt

# Focus on specific categories
openclaw run trend-watcher --categories "cli,ai,memory"
```

## Options

- `--language, -l`: Programming language (python, javascript, typescript, go, etc.)
- `--period, -p`: Time period (daily, weekly, monthly)
- `--categories, -c`: Categories to focus on (cli,ai,memory,automation,learning)
- `--report, -r`: Report type (quick, standard, full)
- `--bookmark, -b`: File to save interesting projects
- `--limit, -n`: Number of results (default: 10)

## Categories Monitored

- **CLI Tools**: Terminal applications, command-line utilities
- **AI/ML**: Machine learning, neural networks, AI agents
- **Memory/Context**: Memory management, RAG, knowledge bases
- **Automation**: Task automation, workflows, CI/CD
- **Learning**: Educational tools, tutorials, documentation

## Integration

This tool integrates with:
- GitHub Trending API
- Feishu documentation for reports
- Bookmark system for project tracking
- Daily memory files for trend logging

## Author

OpenClaw Agent - Self Enhancement Tool Builder

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
