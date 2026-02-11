# feishu-doc

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/autogame-17/feishu-doc/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/autogame-17/feishu-doc/SKILL.md)
> Category: Browser & Automation

---

## Description

Fetch content from Feishu (Lark) Wiki, Docs, Sheets, and Bitable. Automatically resolves Wiki URLs to real entities and converts content to Markdown.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** feishu, lark, wiki, doc, sheet, document, reader

---

## GOTCHA Framework

### G - Goals
Fetch content from Feishu (Lark) Wiki, Docs, Sheets, and Bitable. Automatically resolves Wiki URLs to real entities and converts content to Markdown.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run feishu-doc`)
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
You are executing the feishu-doc workflow. Use the following context:

Description: Fetch content from Feishu (Lark) Wiki, Docs, Sheets, and Bitable. Automatically resolves Wiki URLs to real entities and converts content to Markdown.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: feishu-doc
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Feishu Doc Skill

Fetch content from Feishu (Lark) Wiki, Docs, Sheets, and Bitable.

## Usage

```bash
node index.js fetch <url>
```

## Configuration

Create a `config.json` file in the root of the skill or set environment variables:

```json
{
  "app_id": "YOUR_APP_ID",
  "app_secret": "YOUR_APP_SECRET"
}
```

Environment variables:
- `FEISHU_APP_ID`
- `FEISHU_APP_SECRET`

## Supported URL Types

- Wiki
- Docx
- Doc (Legacy)
- Sheets
- Bitable

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
