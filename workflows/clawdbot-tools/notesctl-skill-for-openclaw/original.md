



# notesctl (Apple Notes, low-token)

## Goal

Minimize token usage and avoid fragile quoting by routing Apple Notes operations through bundled scripts.

## Quick start

### Create a new note (deterministic title/body)

- JSON stdin (recommended):

```bash
echo '{"title":"Title","body":"Line 1\nLine 2","folder":"Notes"}' | {baseDir}/scripts/notes_post.sh
```

- Direct args:

```bash
{baseDir}/scripts/notes_new.sh "Title" $'Body line 1\nBody line 2' "Notes"
```

### List/search/export

```bash
{baseDir}/scripts/notes_list.sh "Notes"
{baseDir}/scripts/notes_search.sh "query" "Notes"
{baseDir}/scripts/notes_export.sh "query" "Notes" "/tmp"  # interactive select then export
```

## Output conventions

- Keep receipts short: `Wrote to Notes: <title>`. 

## Notes on editing

Editing existing notes is inherently more fragile:
- Prefer append workflows or create a new note with a reference.
- If the user explicitly wants interactive editing, use `memo notes -e` (manual selection + editor).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
