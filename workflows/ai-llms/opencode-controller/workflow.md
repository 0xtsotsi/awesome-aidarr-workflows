# opencode-controller

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/karatla/opencode-controller/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/karatla/opencode-controller/SKILL.md)
> Category: AI & LLMs

---

## Description

Control and operate Opencode via slash commands. Use this skill to manage sessions, select models, switch agents (plan/build), and coordinate coding through Opencode.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Control and operate Opencode via slash commands. Use this skill to manage sessions, select models, switch agents (plan/build), and coordinate coding through Opencode.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run opencode-controller`)
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
You are executing the opencode-controller workflow. Use the following context:

Description: Control and operate Opencode via slash commands. Use this skill to manage sessions, select models, switch agents (plan/build), and coordinate coding through Opencode.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: opencode-controller
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Opencode Controller

## Core rule

Clawdbot does not write code.
All planning and coding happens inside Opencode.

## Pre-flight

- Ask the user which AI provider to use.
- Ask how the provider should be authenticated.
- Do not proceed without confirmation.

## Session management

- Start Opencode.
- Open session selector using:
  /sessions
- If the current project already exists:
  - Select the existing session.
- Never create a new session without user approval.

## Agent (mode) control

- Open agent selector using:
  /agents
- Available agents:
  - Plan
  - Build
- Always select Plan first.
- Switch agents whenever required using `/agents`.

## Model selection

- Open model selector using:
  /models
- Select the user-requested provider.
- If authentication is required:
  - Copy the login link provided by Opencode.
  - Send it to the user.
  - Wait for confirmation before continuing.

## Plan agent behavior

- Ask Opencode to analyze the task.
- Request a clear step-by-step plan.
- Allow Opencode to ask clarification questions.
- Review the plan carefully.
- If the plan is incorrect or incomplete:
  - Ask Opencode to revise it.
- Do not allow code generation in Plan.

## Build agent behavior

- Switch to Build using `/agents`.
- Ask Opencode to implement the approved plan.
- If Opencode asks any question:
  - Immediately switch back to Plan.
  - Answer and confirm the plan.
  - Switch back to Build.

## Completion

- Repeat the Plan → Build loop until all user requirements are satisfied.
- Never skip Plan.
- Never answer questions in Build.

## Output format

- Show all slash commands explicitly.
- State which option is selected.
- Provide login links verbatim.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
