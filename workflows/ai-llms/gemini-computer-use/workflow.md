# gemini-computer-use

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/am-will/gemini-computer-use/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/am-will/gemini-computer-use/SKILL.md)
> Category: AI & LLMs

---

## Description

Build and run Gemini 2.5 Computer Use browser-control agents with Playwright. Use when a user wants to automate web browser tasks via the Gemini Computer Use model, needs an agent loop (screenshot → function_call → action → function_response), or asks to integrate safety confirmation for risky UI actions.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Build and run Gemini 2.5 Computer Use browser-control agents with Playwright. Use when a user wants to automate web browser tasks via the Gemini Computer Use model, needs an agent loop (screenshot → function_call → action → function_response), or asks to integrate safety confirmation for risky UI actions.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run gemini-computer-use`)
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
You are executing the gemini-computer-use workflow. Use the following context:

Description: Build and run Gemini 2.5 Computer Use browser-control agents with Playwright. Use when a user wants to automate web browser tasks via the Gemini Computer Use model, needs an agent loop (screenshot → function_call → action → function_response), or asks to integrate safety confirmation for risky UI actions.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: gemini-computer-use
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Gemini Computer Use

## Quick start

1. Source the env file and set your API key:

   ```bash
   cp env.example env.sh
   $EDITOR env.sh
   source env.sh
   ```

2. Create a virtual environment and install dependencies:

   ```bash
   python -m venv .venv
   source .venv/bin/activate
   pip install google-genai playwright
   playwright install chromium
   ```

3. Run the agent script with a prompt:

   ```bash
   python scripts/computer_use_agent.py \
     --prompt "Find the latest blog post title on example.com" \
     --start-url "https://example.com" \
     --turn-limit 6
   ```

## Browser selection

- Default: Playwright's bundled Chromium (no env vars required).
- Choose a channel (Chrome/Edge) with `COMPUTER_USE_BROWSER_CHANNEL`.
- Use a custom Chromium-based executable (e.g., Brave) with `COMPUTER_USE_BROWSER_EXECUTABLE`.

If both are set, `COMPUTER_USE_BROWSER_EXECUTABLE` takes precedence.

## Core workflow (agent loop)

1. Capture a screenshot and send the user goal + screenshot to the model.
2. Parse `function_call` actions in the response.
3. Execute each action in Playwright.
4. If a `safety_decision` is `require_confirmation`, prompt the user before executing.
5. Send `function_response` objects containing the latest URL + screenshot.
6. Repeat until the model returns only text (no actions) or you hit the turn limit.

## Operational guidance

- Run in a sandboxed browser profile or container.
- Use `--exclude` to block risky actions you do not want the model to take.
- Keep the viewport at 1440x900 unless you have a reason to change it.

## Resources

- Script: `scripts/computer_use_agent.py`
- Reference notes: `references/google-computer-use.md`
- Env template: `env.example`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
