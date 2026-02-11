# hn-extract

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/guoqiao/hn-extract/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/guoqiao/hn-extract/SKILL.md)
> Category: Search & Research

---

## Description

Extract a HackerNews post (article + comments) into single clean Markdown for quick reading or LLM input.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Extract a HackerNews post (article + comments) into single clean Markdown for quick reading or LLM input.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run hn-extract`)
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
You are executing the hn-extract workflow. Use the following context:

Description: Extract a HackerNews post (article + comments) into single clean Markdown for quick reading or LLM input.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: hn-extract
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# HackerNews Extract

Extract a HackerNews post (article + comments) into single clean Markdown for quick reading or LLM input.

see [Examples](https://github.com/guoqiao/skills/blob/main/hn-extract/examples)

## What it does
- Accepts an HackerNews id or url
- Download the linked article HTML, cleans and formats it.
- Fetches the Hacknews post metadata and comments.
- Outputs a readable combined markdown file with original article, threaded comments, and key metadata.

## Requirements

- `uv` installed and in PATH.

## Install

No install beyond having `uv`.
Dependencies will be installed automatically by `uv` into to a dedicated venv when run this script.

## Usage Workflow (Mandatory for Agents)

When an agent is asked to extract a HackerNews post:
1.  **Run the script** with an output path: `uv run --script ${baseDir}/hn-extract.py <input> -o /tmp/hn-<id>.md`.
2.  **Send ONE combined message:** Upload the file and ask the question in the *same* tool call. Use the `message` tool (`action=send`, `filePath="/tmp/hn-<id>.md"`, `message="Extraction complete. Do you want me to summarize it?"`).
3.  **Do not** output the full text or a summary directly in the chat unless specifically requested.

## Usage

```bash
# run as uv script
uv run --script ${baseDir}/hn-extract.py <hn-id|hn-url|path/to/item.json> [-o path/to/output.md]

# Examples
uv run --script ${baseDir}/hn-extract.py 46861313 -o /tmp/output.md
uv run --script ${baseDir}/hn-extract.py "https://news.ycombinator.com/item?id=46861313"
```

- Omit `-o` to print to stdout.
- Directories for `-o` are created automatically.

## Notes
- Retries are enabled for HTTP fetches.
- Comments are indented by thread depth.
- Sites requires authentication or blocks scraping may still fail.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
