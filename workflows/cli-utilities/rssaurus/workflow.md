# rssaurus

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/justinburdett/rssaurus/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/justinburdett/rssaurus/SKILL.md)
> Category: CLI Utilities

---

## Description

Use the RSSaurus command-line client (Go binary `rssaurus`) to interact with https://rssaurus.com from the terminal: authenticate (`rssaurus auth login/whoami`), list feeds/items, print item URLs for piping, open URLs, and perform triage actions (mark read/unread, bulk mark-read, save/unsave). Use when asked to automate RSSaurus tasks from CLI, debug token/config issues, or demonstrate command usage.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Use the RSSaurus command-line client (Go binary `rssaurus`) to interact with https://rssaurus.com from the terminal: authenticate (`rssaurus auth login/whoami`), list feeds/items, print item URLs for piping, open URLs, and perform triage actions (mark read/unread, bulk mark-read, save/unsave). Use when asked to automate RSSaurus tasks from CLI, debug token/config issues, or demonstrate command usage.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run rssaurus`)
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
You are executing the rssaurus workflow. Use the following context:

Description: Use the RSSaurus command-line client (Go binary `rssaurus`) to interact with https://rssaurus.com from the terminal: authenticate (`rssaurus auth login/whoami`), list feeds/items, print item URLs for piping, open URLs, and perform triage actions (mark read/unread, bulk mark-read, save/unsave). Use when asked to automate RSSaurus tasks from CLI, debug token/config issues, or demonstrate command usage.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: rssaurus
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# RSSaurus CLI

Use the installed `rssaurus` binary on this machine to interact with RSSaurus.

## Quick checks (when something fails)

1) Confirm binary exists:

```bash
which rssaurus
rssaurus --version || true
```

2) Confirm auth works:

```bash
rssaurus auth whoami
```

### Privacy note

- Do **not** print (e.g. `cat`) the RSSaurus CLI config file contents; it can contain API tokens.
- If auth fails, prefer re-authenticating (`rssaurus auth login`) or asking the user to paste only non-sensitive details (error output, host, etc.).

## Common tasks

### List feeds

```bash
rssaurus feeds
rssaurus feeds --json
```

### List items

Unread by default:

```bash
rssaurus items --limit 20
```

Filter by feed:

```bash
rssaurus items --feed-id 3 --limit 20
```

Machine-friendly URL output (one per line):

```bash
rssaurus items --limit 20 --urls
```

Cursor paging:

```bash
rssaurus items --limit 50 --cursor <cursor>
```

### Open a URL

```bash
rssaurus open https://example.com
```

### Mark read/unread

These require item IDs (get them via `--json`).

```bash
rssaurus items --limit 5 --json
rssaurus read <item-id>
rssaurus unread <item-id>
```

Bulk mark read:

```bash
rssaurus mark-read --all
# or
rssaurus mark-read --ids 1,2,3
# optional
rssaurus mark-read --all --feed-id 3
```

### Save / unsave

```bash
rssaurus save https://example.com --title "Optional title"

# unsave requires an id (obtain via --json output from the API response or future saved-items listing)
rssaurus unsave <saved-item-id>
```

## Output conventions (privacy)

- Default human output avoids printing internal DB IDs.
- Use `--json` output when IDs are required for scripting or write actions.

## References

- CLI repo: https://github.com/RSSaurus/rssaurus-cli
- Homebrew tap: https://github.com/RSSaurus/tap
- Token creation: https://rssaurus.com/api_tokens/new

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
