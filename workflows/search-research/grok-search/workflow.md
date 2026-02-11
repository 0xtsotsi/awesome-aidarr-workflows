# grok-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/notabhay/grok-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/notabhay/grok-search/SKILL.md)
> Category: Search & Research

---

## Description

Search the web or X/Twitter using xAI Grok server-side tools (web_search, x_search) via the xAI Responses API. Use when you need tweets/threads/users from X, want Grok as an alternative to Brave, or you need structured JSON + citations.

**Homepage:** https://docs.x.ai/docs/guides/tools/search-tools
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search the web or X/Twitter using xAI Grok server-side tools (web_search, x_search) via the xAI Responses API. Use when you need tweets/threads/users from X, want Grok as an alternative to Brave, or you need structured JSON + citations.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run grok-search`)
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
You are executing the grok-search workflow. Use the following context:

Description: Search the web or X/Twitter using xAI Grok server-side tools (web_search, x_search) via the xAI Responses API. Use when you need tweets/threads/users from X, want Grok as an alternative to Brave, or you need structured JSON + citations.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: grok-search
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: https://docs.x.ai/docs/guides/tools/search-tools
```

---

## Original Skill Content



Run xAI Grok locally via bundled scripts (search + chat + model listing). Default output for search is *pretty JSON* (agent-friendly) with citations.

## API key

The script looks for an xAI API key in this order:
- `XAI_API_KEY` env var
- `~/.clawdbot/clawdbot.json` → `env.XAI_API_KEY`
- `~/.clawdbot/clawdbot.json` → `skills.entries["grok-search"].apiKey`
- fallback: `skills.entries["search-x"].apiKey` or `skills.entries.xai.apiKey`

## Run

Use `{baseDir}` so the command works regardless of workspace layout.

### Search

- Web search (JSON):
  - `node {baseDir}/scripts/grok_search.mjs "<query>" --web`

- X/Twitter search (JSON):
  - `node {baseDir}/scripts/grok_search.mjs "<query>" --x`

### Chat

- Chat (text):
  - `node {baseDir}/scripts/chat.mjs "<prompt>"`

- Chat (vision):
  - `node {baseDir}/scripts/chat.mjs --image /path/to/image.jpg "<prompt>"`

### Models

- List models:
  - `node {baseDir}/scripts/models.mjs`

## Useful flags

Output:
- `--links-only` print just citation URLs
- `--text` hide the citations section in pretty output
- `--raw` include the raw Responses API payload on stderr (debug)

Common:
- `--max <n>` limit results (default 8)
- `--model <id>` (default `grok-4-1-fast`)

X-only filters (server-side via x_search tool params):
- `--days <n>` (e.g. 7)
- `--from YYYY-MM-DD` / `--to YYYY-MM-DD`
- `--handles @a,@b` (limit to these handles)
- `--exclude @bots,@spam` (exclude handles)

## Output shape (JSON)

```json
{
  "query": "...",
  "mode": "web" | "x",
  "results": [
    {
      "title": "...",
      "url": "...",
      "snippet": "...",
      "author": "...",
      "posted_at": "..."
    }
  ],
  "citations": ["https://..."]
}
```

## Notes

- `citations` are merged/validated from xAI response annotations where possible (more reliable than trusting the model’s JSON blindly).
- Prefer `--x` for tweets/threads, `--web` for general research.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
