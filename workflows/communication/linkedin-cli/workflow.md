# linkedin-cli

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/arun-8687/linkedin-cli/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/arun-8687/linkedin-cli/SKILL.md)
> Category: Communication

---

## Description

A bird-like LinkedIn CLI for searching profiles, checking messages, and summarizing your feed using session cookies.

**Homepage:** https://github.com/clawdbot/linkedin-cli
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
A bird-like LinkedIn CLI for searching profiles, checking messages, and summarizing your feed using session cookies.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run linkedin-cli`)
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
You are executing the linkedin-cli workflow. Use the following context:

Description: A bird-like LinkedIn CLI for searching profiles, checking messages, and summarizing your feed using session cookies.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: linkedin-cli
category: Communication
version: 1.0.0
user_invocable: True
homepage: https://github.com/clawdbot/linkedin-cli
```

---

## Original Skill Content



# LinkedIn CLI (lk)

A witty, punchy LinkedIn CLI inspired by the `bird` CLI. It uses session cookies for authentication, allowing for automated profile scouting, feed summaries, and message checks without a browser.

## Setup

1.  **Extract Cookies**: Open LinkedIn in Chrome/Firefox.
2.  Go to **DevTools (F12)** -> **Application** -> **Cookies** -> `www.linkedin.com`.
3.  Copy the values for `li_at` and `JSESSIONID`.
4.  Set them in your environment:
    ```bash
    export LINKEDIN_LI_AT="your_li_at_value"
    export LINKEDIN_JSESSIONID="your_jsessionid_value"
    ```

## Usage

- `lk whoami`: Display your current profile details.
- `lk search "query"`: Search for people by keywords.
- `lk profile <public_id>`: Get a detailed summary of a specific profile.
- `lk feed -n 10`: Summarize the top N posts from your timeline.
- `lk messages`: Quick peek at your recent conversations.
- `lk check`: Combined whoami and messages check.

## Dependencies

Requires the `linkedin-api` Python package:
```bash
pip install linkedin-api
```

## Authors
- Built by Fido 🐶

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
