# nzbget

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/aricus/nzbget/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/aricus/nzbget/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Check NZBGet download status and queue information. Use when the user asks about NZBGet downloads, wants to know how many things are downloading, check download speed, view the queue, or get a full status report of their Usenet downloads.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Check NZBGet download status and queue information. Use when the user asks about NZBGet downloads, wants to know how many things are downloading, check download speed, view the queue, or get a full status report of their Usenet downloads.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run nzbget`)
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
You are executing the nzbget workflow. Use the following context:

Description: Check NZBGet download status and queue information. Use when the user asks about NZBGet downloads, wants to know how many things are downloading, check download speed, view the queue, or get a full status report of their Usenet downloads.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: nzbget
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# NZBGet Status Checker

This skill provides quick access to NZBGet download status and queue information.  Required env vars: NZBGET_USER, NZBGET_PASS, NZBGET_HOST

## Usage

### Quick Count
Get a simple count of active downloads:
```bash
bash scripts/check_nzbget.sh count
```
Returns: `3` (number of items downloading)

### Full Status Report
Get complete status with speed, queue, and remaining size:
```bash
bash scripts/check_nzbget.sh
```

### Specific Queries

| Query | Command | Output |
|-------|---------|--------|
| How many downloading? | `count` | Number only |
| Current speed? | `speed` | Speed in MB/s |
| What's in queue? | `queue` | First 10 items only |
| Full status | (no args) | Complete report (max 10 items shown) |

**Note:** Queue listings are capped at 10 items to avoid flooding with large queues (400+ items). The script shows "Next 10 of X items" when there are more.

## Examples

**User:** "NZBGet count"
```
3
```

**User:** "What's downloading?"
```
📥 NZBGet Status: Downloading

Active Downloads: 3
Speed: 12.5 MB/s
Remaining: 45.2 GB

Current Queue:
  • Movie.2025.2160p.mkv - 67%
  • TV.Show.S01E05.1080p.mkv - 23%
  • Documentary.4K.mkv - 89%
```

**User:** "NZBGet speed"
```
12.5 MB/s
```

## Response Guidelines

- For "count" or "how many": Use the number directly in a conversational response
- For "speed": Report the current download speed
- For full status: Summarize the key info (count, speed, remaining) and list active items
- If NZBGet is unreachable or no items downloading, say so clearly
- Keep responses concise unless user asks for full details

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
