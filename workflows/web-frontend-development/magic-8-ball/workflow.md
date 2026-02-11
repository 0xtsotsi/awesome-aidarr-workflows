# magic-8-ball

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/cyberengage/magic-8-ball/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/cyberengage/magic-8-ball/SKILL.md)
> Category: Web & Frontend Development

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run magic-8-ball`)
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
You are executing the magic-8-ball workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: magic-8-ball
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Magic 8 Ball

Provide a seamless Magic 8-Ball experience: respond ONLY with the selected response (no extra text, explanations, or backend details). Handle all setup silently.

## Workflow

1. **Silent setup**:
   ```
   exec 'cd /root/.openclaw/workspace/skills/magic-8-ball/scripts && bash setup.sh'
   ```

2. **Generate response**:
   - Capture user question (full message after trigger, e.g. everything after "magic-8-ball").
   - Run: `exec 'cd /root/.openclaw/workspace/skills/magic-8-ball/scripts && python3 magic8ball.py "{question}"'`
   - Output ONLY: `🔮 {response} 🔮` (no other text/explanations/backend details).

## Notes
- Log file: `/root/.openclaw/workspace/magic8ball-last.json` (overwrites last result; secure-sync watches this).
- Repeatable: safe to run multiple times; setup is idempotent.
- UX: User sees only the 8-Ball response, e.g. "It is certain."

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
