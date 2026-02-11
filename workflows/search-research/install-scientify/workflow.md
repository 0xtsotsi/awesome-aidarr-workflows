# install-scientify

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/springleave/install-scientify/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/springleave/install-scientify/SKILL.md)
> Category: Search & Research

---

## Description

Install Scientify - AI-powered research workflow automation plugin. Adds skills for idea-generation, literature-review, research-pipeline, arxiv search, and workspace management commands.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Install Scientify - AI-powered research workflow automation plugin. Adds skills for idea-generation, literature-review, research-pipeline, arxiv search, and workspace management commands.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run install-scientify`)
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
You are executing the install-scientify workflow. Use the following context:

Description: Install Scientify - AI-powered research workflow automation plugin. Adds skills for idea-generation, literature-review, research-pipeline, arxiv search, and workspace management commands.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: install-scientify
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Install Scientify

**Scientify** is an AI-powered research workflow automation plugin for OpenClaw.

## What You Get

### Skills (LLM-powered)

| Skill | Description |
|-------|-------------|
| **idea-generation** | Generate innovative research ideas. Searches arXiv/GitHub, downloads papers, analyzes literature, outputs 5 ideas with citations. |
| **research-pipeline** | End-to-end ML research workflow: idea → literature → survey → plan → implement → review → iterate. |
| **literature-review** | Generate structured notes and synthesis from collected papers. |
| **arxiv** | Search arXiv.org for papers and download .tex sources. |

### Commands (Direct, no LLM)

| Command | Description |
|---------|-------------|
| `/research-status` | Show workspace status |
| `/papers` | List downloaded papers |
| `/ideas` | List generated ideas |
| `/projects` | List all projects |
| `/project-switch <id>` | Switch project |
| `/project-delete <id>` | Delete project |

### Tool

- **arxiv** - Search arXiv.org API with keyword search, date filtering, automatic .tex download

## Installation

Run:

```bash
npm install -g scientify
```

Or let OpenClaw install it automatically when you use this skill.

Then add to your OpenClaw config:

```json
{
  "plugins": ["scientify"]
}
```

## Usage Examples

### Generate Research Ideas

```
帮我调研 "长文档摘要" 领域，生成一些创新的研究想法
```

### Daily Literature Tracking

```
帮我设置一个定时任务，每天检查 arXiv 上关于 "transformer efficiency" 的新论文，发到飞书
```

### Check Workspace

```
/research-status
```

## Links

- npm: https://www.npmjs.com/package/scientify
- GitHub: https://github.com/tsingyuai/scientific
- Author: tsingyuai

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
