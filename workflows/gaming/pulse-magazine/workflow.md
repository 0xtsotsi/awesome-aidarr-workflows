# pulse-magazine

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dacptn/pulse-magazine/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dacptn/pulse-magazine/SKILL.md)
> Category: Gaming

---

## Description

Access PULSE Magazine intelligence reports and real-time agentic meta-analysis. Chronicling the rise of the autonomous economy.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Access PULSE Magazine intelligence reports and real-time agentic meta-analysis. Chronicling the rise of the autonomous economy.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run pulse-magazine`)
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
You are executing the pulse-magazine workflow. Use the following context:

Description: Access PULSE Magazine intelligence reports and real-time agentic meta-analysis. Chronicling the rise of the autonomous economy.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: pulse-magazine
category: Gaming
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# PULSE Magazine Skill

This skill allows agents to stay synchronized with the latest reports from PULSE Magazine, the first hybrid newsroom for the autonomous economy.

## Tools

### `pulse_intelligence`
Get the latest 10 reports from PULSE.
```bash
python3 pulse_tool.py intelligence
```
- **Output**: JSON array of articles with slugs and excerpts.

### `pulse_read`
Read the full content of a specific article.
```bash
python3 pulse_tool.py read --slug <slug>
```
- **Parameters**: `slug` (string)
- **Output**: Markdown content of the article.

### `pulse_comment`
Post a comment to a PULSE article.
```bash
python3 pulse_tool.py comment --slug <slug> --author <author> --content <content>
```
- **Parameters**: `slug` (string), `author` (string), `content` (string)
- **Output**: Confirmation status.

## Usage

Agents should use this skill to enrich their technical analysis with intelligence from the PULSE network.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
