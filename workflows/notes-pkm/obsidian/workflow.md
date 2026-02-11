# obsidian

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/obsidian/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/obsidian/SKILL.md)
> Category: Notes & PKM

---

## Description

Work with Obsidian vaults (plain Markdown notes) and automate via obsidian-cli.

**Homepage:** https://help.obsidian.md
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Work with Obsidian vaults (plain Markdown notes) and automate via obsidian-cli.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run obsidian`)
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
You are executing the obsidian workflow. Use the following context:

Description: Work with Obsidian vaults (plain Markdown notes) and automate via obsidian-cli.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: obsidian
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: https://help.obsidian.md
```

---

## Original Skill Content



# Obsidian

Obsidian vault = a normal folder on disk.

Vault structure (typical)
- Notes: `*.md` (plain text Markdown; edit with any editor)
- Config: `.obsidian/` (workspace + plugin settings; usually don’t touch from scripts)
- Canvases: `*.canvas` (JSON)
- Attachments: whatever folder you chose in Obsidian settings (images/PDFs/etc.)

## Find the active vault(s)

Obsidian desktop tracks vaults here (source of truth):
- `~/Library/Application Support/obsidian/obsidian.json`

`obsidian-cli` resolves vaults from that file; vault name is typically the **folder name** (path suffix).

Fast “what vault is active / where are the notes?”
- If you’ve already set a default: `obsidian-cli print-default --path-only`
- Otherwise, read `~/Library/Application Support/obsidian/obsidian.json` and use the vault entry with `"open": true`.

Notes
- Multiple vaults common (iCloud vs `~/Documents`, work/personal, etc.). Don’t guess; read config.
- Avoid writing hardcoded vault paths into scripts; prefer reading the config or using `print-default`.

## obsidian-cli quick start

Pick a default vault (once):
- `obsidian-cli set-default "<vault-folder-name>"`
- `obsidian-cli print-default` / `obsidian-cli print-default --path-only`

Search
- `obsidian-cli search "query"` (note names)
- `obsidian-cli search-content "query"` (inside notes; shows snippets + lines)

Create
- `obsidian-cli create "Folder/New note" --content "..." --open`
- Requires Obsidian URI handler (`obsidian://…`) working (Obsidian installed).
- Avoid creating notes under “hidden” dot-folders (e.g. `.something/...`) via URI; Obsidian may refuse.

Move/rename (safe refactor)
- `obsidian-cli move "old/path/note" "new/path/note"`
- Updates `[[wikilinks]]` and common Markdown links across the vault (this is the main win vs `mv`).

Delete
- `obsidian-cli delete "path/note"`

Prefer direct edits when appropriate: open the `.md` file and change it; Obsidian will pick it up.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
