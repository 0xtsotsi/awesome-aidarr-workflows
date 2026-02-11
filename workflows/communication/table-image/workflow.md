# table-image

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/joargp/table-image/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/joargp/table-image/SKILL.md)
> Category: Communication

---

## Description

Generate images from tables for better readability in messaging apps like Telegram. Use when displaying tabular data.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate images from tables for better readability in messaging apps like Telegram. Use when displaying tabular data.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run table-image`)
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
You are executing the table-image workflow. Use the following context:

Description: Generate images from tables for better readability in messaging apps like Telegram. Use when displaying tabular data.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: table-image
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Table Image Skill

Render markdown tables as PNG images for messaging platforms that don't support markdown tables.

## Prerequisites

Install tablesnap:

```bash
go install github.com/joargp/tablesnap/cmd/tablesnap@latest
```

Or build from source:
```bash
git clone https://github.com/joargp/tablesnap.git
cd tablesnap
go build -o tablesnap ./cmd/tablesnap
```

## Usage

```bash
echo "| Header 1 | Header 2 |
|----------|----------|
| Data 1   | Data 2   |" | tablesnap -o /tmp/table.png
```

Then send with `MEDIA:/tmp/table.png`

## Options

| Flag | Default | Description |
|------|---------|-------------|
| `-i` | stdin | Input file |
| `-o` | stdout | Output file |
| `--theme` | dark | Theme: `dark` or `light` |
| `--font-size` | 14 | Font size in pixels |
| `--padding` | 10 | Cell padding in pixels |

## Emoji Support

**Bundled** (work out of the box): ✅ ❌ 🔴 🟢 🟡 ⭕ ⚠️

**Full emoji** (one-time download):
```bash
tablesnap emojis install
```

Unsupported emoji render as □ until full set is installed.

## Example Workflow

```bash
# Create table image
echo "| Task | Status |
|------|--------|
| Build | ✅ |
| Deploy | 🚀 |" | tablesnap -o /tmp/table.png

# Send in reply
MEDIA:/tmp/table.png
```

## Notes

- Dark theme by default (matches Telegram/Discord dark mode)
- Auto-sizes to fit content
- Output ~10-20KB (messaging-friendly)
- Cross-platform (Inter font embedded)

## Links

- [tablesnap repo](https://github.com/joargp/tablesnap)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
