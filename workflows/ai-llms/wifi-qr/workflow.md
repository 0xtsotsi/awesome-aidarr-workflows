# wifi-qr

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xejrax/wifi-qr/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xejrax/wifi-qr/SKILL.md)
> Category: AI & LLMs

---

## Description

Generate QR code for Wi-Fi credentials

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate QR code for Wi-Fi credentials

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run wifi-qr`)
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
You are executing the wifi-qr workflow. Use the following context:

Description: Generate QR code for Wi-Fi credentials

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: wifi-qr
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Wi-Fi QR

Generate a QR code for Wi-Fi credentials. Scan the QR code with a phone to instantly connect to the network without typing the password.

## Commands

```bash
# Generate a QR code for a Wi-Fi network (defaults to WPA)
wifi-qr "MyNetwork" "mypassword"

# Specify the security type explicitly
wifi-qr "MyNetwork" "mypassword" --type WPA
```

## Install

```bash
sudo dnf install qrencode
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
