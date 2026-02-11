# telecom-agent-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kflohr/telecom-agent-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kflohr/telecom-agent-skill/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Turn your AI Agent into a Telecom Operator. Bulk calling, ChatOps, and Field Monitoring.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.2.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Turn your AI Agent into a Telecom Operator. Bulk calling, ChatOps, and Field Monitoring.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run telecom-agent-skill`)
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
You are executing the telecom-agent-skill workflow. Use the following context:

Description: Turn your AI Agent into a Telecom Operator. Bulk calling, ChatOps, and Field Monitoring.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: telecom-agent-skill
category: DevOps & Cloud
version: 1.2.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# 📡 Telecom Agent Skill v1.2

**Give your MoltBot / OpenClaw agent the power of a Telecom Operator.**

This skill connects your agent to the **Telecom Operator Console**, allowing it to manage campaigns, handle approvals, and operate on the public telephone network safely.

## ✨ Capabilities

### 🚀 Campaign Queue (Bulk Calling) *New*
*   **Mass Dialing**: Upload a list of 10,000+ numbers. The system handles rate-limiting.
*   **ChatOps**: "Bot, create a campaign for the 'Friday Leads' list."
*   **Monitoring**: Agent can poll status with `--json` for precise progress tracking.

### 🗣️ Voice & Speech
*   **Make Calls**: Dial any global number.
*   **Speak**: Dynamic "Text-to-Speech" intro messages.
*   **Listen**: Records audio automatically for quality assurance.

### 📱 Field Operations (Telegram)
*   **Remote Admin**: Monitor system status from a Telegram Bot.
*   **Approvals**: Approve/Deny high-risk actions via mobile buttons.

### 🧠 Operational Memory
*   **Transcripts**: Agent can read full call transcripts (`telecom agent memory`).
*   **Persistence**: All logs saved to the secure Operator Console.

---

## 🚀 Quick Start for Agents

### 1. Installation
```bash
/install https://github.com/kflohr/telecom-agent-skill
```

### 2. Setup
```bash
telecom onboard
# Follow the wizard to link your Twilio account.
```

### 3. Usage Examples

**Bulk Campaign**:
```bash
telecom campaign create "Outreach" --file leads.csv
telecom campaign status <id> --json
```

**Single Call**:
```bash
telecom agent call +14155550100 --intro "Hello from the AI team."
```

**Memory Retrieval**:
```bash
telecom agent memory <CallSid>
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
