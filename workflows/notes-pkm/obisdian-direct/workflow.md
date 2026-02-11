# obisdian-direct

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ruslanlanket/obisdian-direct/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ruslanlanket/obisdian-direct/SKILL.md)
> Category: Notes & PKM

---

## Description

Work with Obsidian vaults as a knowledge base. Features: fuzzy/phonetic search across all notes, auto-folder detection for new notes, create/read/edit notes with frontmatter, manage tags and wikilinks. Use when: querying knowledge base, saving notes/documents, editing existing notes by user instructions.


**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Work with Obsidian vaults as a knowledge base. Features: fuzzy/phonetic search across all notes, auto-folder detection for new notes, create/read/edit notes with frontmatter, manage tags and wikilinks. Use when: querying knowledge base, saving notes/documents, editing existing notes by user instructions.


### O - Orchestration
**Trigger:** User-invocable (via `aidarr run obisdian-direct`)
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
You are executing the obisdian-direct workflow. Use the following context:

Description: Work with Obsidian vaults as a knowledge base. Features: fuzzy/phonetic search across all notes, auto-folder detection for new notes, create/read/edit notes with frontmatter, manage tags and wikilinks. Use when: querying knowledge base, saving notes/documents, editing existing notes by user instructions.


Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: obisdian-direct
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Obsidian Knowledge Base

Obsidian vault = folder with Markdown files + `.obsidian/` config.

## Configuration

- **Vault Path:** `/home/ruslan/webdav/data/ruslain`
- **Env:** `OBSIDIAN_VAULT=/home/ruslan/webdav/data/ruslain`

## CLI Usage

Scripts location: `/home/ruslan/.openclaw/workspace/skills/obsidian/scripts`

Note: Global flags (`--vault`, `--json`) must come BEFORE the command.

```bash
export OBSIDIAN_VAULT=/home/ruslan/webdav/data/ruslain
cd /home/ruslan/.openclaw/workspace/skills/obsidian/scripts

# Search (fuzzy/phonetic) - uses ripgrep for speed
python3 obsidian_search.py "$OBSIDIAN_VAULT" "query" --limit 10 --json

# List notes
python3 obsidian_cli.py --json list                    # all notes
python3 obsidian_cli.py --json list "Projects"         # in folder

# List folders
python3 obsidian_cli.py --json folders

# Read note
python3 obsidian_cli.py --json read "Note Name"

# Create note
python3 obsidian_cli.py --json create "Title" -c "Content" -f "Folder" -t tag1 tag2
python3 obsidian_cli.py --json create "Title" -c "Content" --auto-folder  # auto-detect folder

# Edit note
python3 obsidian_cli.py --json edit "Note" append -c "Text to append"
python3 obsidian_cli.py --json edit "Note" prepend -c "Text at start"
python3 obsidian_cli.py --json edit "Note" replace -c "New full content"
python3 obsidian_cli.py --json edit "Note" replace-section -s "Summary" -c "New section text"

# Tags
python3 obsidian_cli.py --json tags

# Links (incoming/outgoing)
python3 obsidian_cli.py --json links "Note Name"

# Suggest folder for content
python3 obsidian_cli.py --json suggest-folder "content text" --title "Note Title"
```

## Workflow: Query Knowledge Base

1. Run `obsidian_search.py` with user query
2. Read top results if needed for context
3. Formulate answer based on found content
4. Cite sources: `[[Note Name]]`

## Workflow: Save Note

1. If no folder specified → run `suggest-folder` or use `--auto-folder`
2. Create note with `create` command
3. Add appropriate tags based on content
4. Report created path to user

## Workflow: Edit Note by Prompt

User prompts like:
- "Добавь резюме в конец заметки X" → `edit X append -c "..."`
- "Перепиши заметку Y более кратко" → read note, rewrite, `edit Y replace -c "..."`
- "Добавь секцию 'Выводы' в заметку Z" → `edit Z replace-section -s "Выводы" -c "..."`

## Note Format

```markdown
---
created: 2024-01-15T10:30:00
modified: 2024-01-15T12:00:00
tags:
  - project
  - work
---

# Title

Content with [[wikilinks]] and #inline-tags.
```

## Wikilinks

- `[[Note Name]]` — link to note
- `[[Note Name|Display Text]]` — link with alias
- `[[Note Name#Section]]` — link to section

## Frontmatter Fields

Standard fields:
- `created` — creation timestamp
- `modified` — last edit timestamp  
- `tags` — list of tags
- `aliases` — alternative names for linking

## Search Behavior

`obsidian_search.py` uses:
- ripgrep for fast initial filtering
- Title matching (highest weight)
- Tag matching
- Fuzzy content search with phonetic transliteration (RU↔EN)
- Returns: path, title, score, matched context

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
