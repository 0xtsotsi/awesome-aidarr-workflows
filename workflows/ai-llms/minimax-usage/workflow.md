# minimax-usage

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/thesethrose/minimax-usage/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/thesethrose/minimax-usage/SKILL.md)
> Category: AI & LLMs

---

## Description

Monitor Minimax Coding Plan usage to stay within API limits. Fetches current usage stats and provides status alerts.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Monitor Minimax Coding Plan usage to stay within API limits. Fetches current usage stats and provides status alerts.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run minimax-usage`)
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
You are executing the minimax-usage workflow. Use the following context:

Description: Monitor Minimax Coding Plan usage to stay within API limits. Fetches current usage stats and provides status alerts.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: minimax-usage
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Minimax Usage Skill

Monitor Minimax Coding Plan usage to stay within limits.

## Setup

Create a `.env` file in the same directory as the script:

```bash
MINIMAX_CODING_API_KEY=your_api_key_here
MINIMAX_GROUP_ID=your_group_id_here
```

Get your GroupId from: https://platform.minimax.io/user-center/basic-information (under "Basic Information")

## Usage

```bash
./minimax-usage.sh
```

## Output Example

```
🔍 Checking Minimax Coding Plan usage...
✅ Usage retrieved successfully:

📊 Coding Plan Status (MiniMax-M2):
   Used:      255 / 1500 prompts (17%)
   Remaining: 1245 prompts
   Resets in: 3h 17m

💚 GREEN: 17% used. Plenty of buffer.
```

## API Details

**Endpoint:**
```
GET https://platform.minimax.io/v1/api/openplatform/coding_plan/remains?GroupId={GROUP_ID}
```

**Required Headers:**
```
accept: application/json, text/plain, */*
authorization: Bearer {MINIMAX_CODING_API_KEY}
referer: https://platform.minimax.io/user-center/payment/coding-plan
user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36
```

## Limits

| Metric | Value |
|--------|-------|
| Reset window | 5 hours (dynamic) |
| Max target | 60% usage |
| 1 prompt ≈ | 15 model calls |

## Notes

- Coding Plan API key is **exclusive** to this plan (not interchangeable with standard API keys)
- Usage from 5+ hours ago is automatically released from the count

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
