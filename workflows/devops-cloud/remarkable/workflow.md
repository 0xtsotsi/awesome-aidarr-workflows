# remarkable

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/nickian/remarkable/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/nickian/remarkable/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Send files and web articles to a reMarkable e-ink tablet via the reMarkable Cloud. Upload PDFs, EPUBs, or convert web articles to readable ebooks and send them to the device. Also browse and manage files on the device. Use when the user mentions reMarkable, wants to send an article or document to their e-reader, or manage reMarkable cloud files.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Send files and web articles to a reMarkable e-ink tablet via the reMarkable Cloud. Upload PDFs, EPUBs, or convert web articles to readable ebooks and send them to the device. Also browse and manage files on the device. Use when the user mentions reMarkable, wants to send an article or document to their e-reader, or manage reMarkable cloud files.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run remarkable`)
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
You are executing the remarkable workflow. Use the following context:

Description: Send files and web articles to a reMarkable e-ink tablet via the reMarkable Cloud. Upload PDFs, EPUBs, or convert web articles to readable ebooks and send them to the device. Also browse and manage files on the device. Use when the user mentions reMarkable, wants to send an article or document to their e-reader, or manage reMarkable cloud files.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: remarkable
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# reMarkable Cloud

Send documents and web articles to a reMarkable tablet via the cloud API. Uses `rmapi` for cloud access.

## Setup

Install rmapi (Go required):
```bash
cd /tmp && git clone --depth 1 https://github.com/ddvk/rmapi.git
cd rmapi && go build -o /usr/local/bin/rmapi .
```

First run will prompt for a one-time code from https://my.remarkable.com/device/browser?showOtp=true

Python dependencies (for article conversion): `readability-lxml`, `ebooklib`, `requests`, `beautifulsoup4`, `lxml`.

## Commands

### Send a web article to the device

```bash
{baseDir}/scripts/remarkable.sh send-article --url "https://example.com/article" --dir /Articles
{baseDir}/scripts/remarkable.sh send-article --url "https://example.com/article" --format pdf --dir /
{baseDir}/scripts/remarkable.sh send-article --url "https://example.com/article" --title "Custom Title" --dir /Articles
```

Fetches article, extracts readable content, converts to EPUB (default) or PDF, uploads to reMarkable cloud. Device syncs automatically.

### List files

```bash
{baseDir}/scripts/remarkable.sh ls /
{baseDir}/scripts/remarkable.sh ls /Articles
{baseDir}/scripts/remarkable.sh ls "/Book Notes"
```

Output: `[f]` = file, `[d]` = directory.

### Upload a file

```bash
{baseDir}/scripts/remarkable.sh upload --file /path/to/document.pdf --dir /Books
{baseDir}/scripts/remarkable.sh upload --file /path/to/book.epub --dir /
```

### Create a folder

```bash
{baseDir}/scripts/remarkable.sh mkdir --path /NewFolder
```

### Search for files

```bash
{baseDir}/scripts/remarkable.sh find --name "article title"
```

## Notes

- EPUB is recommended for articles — reflows nicely on e-ink
- Device syncs automatically when connected to WiFi
- Auth tokens are cached by rmapi at `~/.rmapi`
- Some sites block scraping — if article fetch fails, try a different URL

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
