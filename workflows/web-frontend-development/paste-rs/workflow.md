# paste-rs

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/banghasan/paste-rs/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/banghasan/paste-rs/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Paste text, Markdown, or HTML snippets to https://paste.rs and return a shareable URL. Use when the user asks to "paste"/"upload" text to paste.rs, share logs/config snippets safely as a link, or quickly publish command output without sending long messages.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Paste text, Markdown, or HTML snippets to https://paste.rs and return a shareable URL. Use when the user asks to "paste"/"upload" text to paste.rs, share logs/config snippets safely as a link, or quickly publish command output without sending long messages.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run paste-rs`)
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
You are executing the paste-rs workflow. Use the following context:

Description: Paste text, Markdown, or HTML snippets to https://paste.rs and return a shareable URL. Use when the user asks to "paste"/"upload" text to paste.rs, share logs/config snippets safely as a link, or quickly publish command output without sending long messages.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: paste-rs
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# paste.rs

## Quick start (preferred)

Use the bundled script (it **saves a local `.md` file first**, then uploads):

```bash
# paste from stdin
some_command | python3 skills/paste-rs/scripts/paste_rs.py

# paste a file
python3 skills/paste-rs/scripts/paste_rs.py --file ./notes.md

# paste an inline snippet
python3 skills/paste-rs/scripts/paste_rs.py --text '<h1>Hello</h1>'

# choose where the .md file is saved (default: /tmp)
python3 skills/paste-rs/scripts/paste_rs.py --outdir ./tmp-pastes --text 'hello'
```

Output:
- **stdout**: URL `https://paste.rs/XXXX.md`
- **stderr**: path `saved: /tmp/paste-rs-YYYYMMDD-HHMMSS.md`

## Curl one-liners (fallback)

```bash
# stdin
some_command | curl -fsS https://paste.rs -d @-

# file
curl -fsS https://paste.rs -d @./file.txt
```

## Safety notes

- Treat the pasted content as **public**.
- Script `scripts/paste_rs.py` melakukan **redact otomatis by default** untuk pola rahasia umum (token/apiKey/botToken/password/Authorization).
- Kalau memang butuh raw (tidak disarankan), pakai `--no-redact`.

## Resources

- `scripts/paste_rs.py`: deterministic uploader (stdin / --text / --file)
- `references/paste-rs-api.md`: minimal API reference

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
