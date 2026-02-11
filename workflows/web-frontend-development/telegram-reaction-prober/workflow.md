# telegram-reaction-prober

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/deadlysilent/telegram-reaction-prober/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/deadlysilent/telegram-reaction-prober/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Probe which emoji reactions are accepted in a specific Telegram chat/message, record an allow/deny list, and optionally remove test reactions afterwards.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Probe which emoji reactions are accepted in a specific Telegram chat/message, record an allow/deny list, and optionally remove test reactions afterwards.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run telegram-reaction-prober`)
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
You are executing the telegram-reaction-prober workflow. Use the following context:

Description: Probe which emoji reactions are accepted in a specific Telegram chat/message, record an allow/deny list, and optionally remove test reactions afterwards.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: telegram-reaction-prober
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Telegram Reaction Prober

## What this skill is
Telegram reactions are **chat-specific**: a bot can only react with emojis that are enabled for that chat/message. When you try an unsupported emoji, Telegram returns:

- `400 Bad Request: REACTION_INVALID`

This skill is the *prober* (the method + starter datasets), not a global list.
It helps you:
- test a list of candidate emojis against a specific `message_id`
- classify them as **Allowed** vs **Rejected**
- optionally remove successful reactions after testing (so you don't spam the chat)
- write the results into `TOOLS.md` (or another file)

> Important: **Do not publish your private chat’s allow/deny list** as “the answer for everyone”.
> Share the prober + candidate sets; each user still probes their own chat.

## Limits / Reality check
There is no practical way to "test every emoji" (Unicode is enormous, and this Clawdbot Telegram integration does not expose Telegram's enabled-reaction list directly).

So the best approach is:
1) Test a **curated emoji set** you care about (common reactions)
2) Save the whitelist for that chat
3) Re-run when Telegram chat settings change

## How to run (manual)
1) Pick a target Telegram `message_id` (e.g. the most recent message in the chat).
2) Pick a candidate emoji set:
   - start small (15–30), or
   - use the included 200-emoji starter list:
     - `skills/telegram-reaction-prober/assets/emoji200-unicode-frequency-2019.txt`
3) For each emoji:
   - call `message` tool with `action=react` and that emoji
   - if it succeeds → mark Allowed
   - if it fails with `REACTION_INVALID` → mark Rejected
4) Cleanup options:
   - **Fast/quiet:** don’t remove; Telegram generally keeps only one reaction per user/bot (so you’re effectively just flipping it)
   - **Clean:** remove successful reactions after testing via `remove=true`
5) Write results to `/home/ubuntu/clawd/TOOLS.md` under a heading like:
   - `### Telegram reactions (this chat) — tested on message_id XYZ`

## Suggested starter emoji set
Allowed in many chats:
- 👍 ❤️ 🔥 🙏 🎉 🤔 👀

Often rejected (depends on chat):
- ✅ 😂 💡

Good candidates to test next:
- 👎 😅 😭 😮 😍 🤝 👏 🙌 💯 😡 😴 🧠 🧩 ⚠️

## Notes
- Be mindful of rate limits; don’t blast 100+ reactions without delays.
- Keep tests on a single known `message_id` and record it.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
