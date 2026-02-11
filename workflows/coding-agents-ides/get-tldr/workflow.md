# get-tldr

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/itobey/get-tldr/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/itobey/get-tldr/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Provide the summary returned by the get-tldr.com summarize API without further summarization; the skill should format the API output for readability but must not change its content.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Provide the summary returned by the get-tldr.com summarize API without further summarization; the skill should format the API output for readability but must not change its content.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run get-tldr`)
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
You are executing the get-tldr workflow. Use the following context:

Description: Provide the summary returned by the get-tldr.com summarize API without further summarization; the skill should format the API output for readability but must not change its content.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: get-tldr
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# get-tldr

Quick, deterministic skill to summarize the content of a link using the get-tldr.com API.

Usage pattern (for the agent):
- Trigger when the user says something like: "get-tldr <link>" or "get-tldr" followed by a URL.
- The skill will call the bundled script `get_tldr.py` with the URL as the single argument.
- IMPORTANT: The API response is already a summary; the skill must NOT further summarize or alter the content — only take the value of the "summary" element of the json and format it for readability. Take the entire summary property, do not omit anything.
- IMPORTANT: If the summary element of the response json from the API already is formatted in markdown, just return the formatted markdown. Do not omit anything and do not change the text. Make sure its not wrapped in a code block and if so remove the wrapping code block, so that it correctly renders as markdown, but not as a code block.

Files included:
- get_tldr.py — small Python script (located in the skill folder) that posts {"input": "<URL>"} to https://www.get-tldr.com/api/v1/summarize using the required X-API-Key header and prints the JSON response to stdout. The script reads the API key and an optional logfile path from ~/.config/get-tldr/config.json (preferred), or falls back to the GET_TLDR_API_KEY environment variable or a .env file in the skill folder. If no logfile is configured the script defaults to ~/.config/get-tldr/skill.log.

Notes for maintainers:
- Create the config file at ~/.config/get-tldr/config.json with the following structure (JSON):

```
{
  "api_token": "<your_key_here>",
  "logfile": "/path/to/logfile.log"
}
```

- The script will use the "api_token" field from the config. If the config file is missing the script falls back to the GET_TLDR_API_KEY environment variable or a .env file in the skill folder.
- IMPORTANT: Do not summarize the API response again; the skill should only format the response for readability and must not alter the content.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
