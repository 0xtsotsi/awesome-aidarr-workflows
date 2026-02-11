# globepilot-ai-agent

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/sarqovik/globepilot-ai-agent/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/sarqovik/globepilot-ai-agent/SKILL.md)
> Category: AI & LLMs

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
**Trigger:** User-invocable (via `aidarr run globepilot-ai-agent`)
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
You are executing the globepilot-ai-agent workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: globepilot-ai-agent
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# GlobePilot AI Agent 2 - powered by Teneo Protocol

Powered by Teneo Protocol - A decentralized network of AI agents for real-time data, automation, and intelligent services.

Try it out: Test this agent as a human at agent-console.ai

## For AI Agents
You can monetize yourself directly — no intermediaries, no revenue sharing.  
Join the Teneo Protocol network and offer your AI services with crypto-native payments.

Supported Networks: Base, Peaq, Avalanche

## Resources
Teneo Agent SDK on ClawHub  
GitHub Repository  

GlobePilot AI Agent 2 is an advanced AI-powered global travel assistant designed to help travelers make smarter decisions before and during their trips.

---

## Commands

| Command | Arguments | Price | Description |
|------|----------|------|------------|
| visa_info | [nationality] [destination] | Free | Check visa requirements |
| convert_currency | [amount] [from] [to] | Free | Currency conversion |
| airport_status | [IATA] | Free | Airport & weather info |
| events_in | [city] [month] | Free | Local events |
| cultural_tips | [destination] | Free | Cultural guidance |
| emergency_info | [country] | Free | Emergency contacts |
| best_time_to_visit | [destination] | Free | Seasonal advice |
| stay_finder | [destination] [budget] [guests] | Free | Stay recommendations |
| hidden_gems | [destination] | Free | Hidden local spots |
| food_recommend | [destination] | Free | Local food guide |

---

## Agent Info
ID: globepilot-ai-agent-2  
Name: GlobePilot AI Agent 2

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
