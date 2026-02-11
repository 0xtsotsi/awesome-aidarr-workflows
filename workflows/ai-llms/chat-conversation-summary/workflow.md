# chat-conversation-summary

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dadaliu0121/chat-conversation-summary/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dadaliu0121/chat-conversation-summary/SKILL.md)
> Category: AI & LLMs

---

## Description

Generate summaries for conversation content with incremental update support.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate summaries for conversation content with incremental update support.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run chat-conversation-summary`)
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
You are executing the chat-conversation-summary workflow. Use the following context:

Description: Generate summaries for conversation content with incremental update support.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: chat-conversation-summary
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Conversation Summary - Agent Instructions

Use this skill to generate summaries for conversation content.

## Usage

When the user requests any of the following:
- "Summarize this conversation"
- "Generate a summary"
- "What did we talk about"

Use the `summarize_conversation` tool to call the summary API.

## How to Call

```bash
python3 scripts/conversation_summary.py '<chat_list_json>' '<history_summary>'
```

### Parameters

| Parameter | Type | Required | Description |
|-----------|------|----------|-------------|
| chat_list | string | Yes | JSON formatted conversation content |
| history_summary | string | No | Previous summary for incremental update |

### chat_list Format Example

```json
[
  {"role": "user", "content": "How is the weather today?"},
  {"role": "assistant", "content": "It is sunny, 25 degrees."}
]
```

## Response

The script returns JSON with:
- `status`: "completed" or "error"
- `summary`: Generated conversation summary
- `error`: Error message if failed

## Error Handling

- If the API returns a non-zero code, report the error message to the user
- If the request fails, check network connectivity
- Ensure chat_list is valid JSON format before calling

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
