# crawsecure

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/diogopaesdev/crawsecure/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/diogopaesdev/crawsecure/SKILL.md)
> Category: DevOps & Cloud

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
**Trigger:** User-invocable (via `aidarr run crawsecure`)
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
You are executing the crawsecure workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: crawsecure
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

Offline security scanner for ClawHub skills — detect unsafe patterns before installation.

# CrawSecure

CrawSecure is an **offline security analysis skill** designed to help users evaluate potential risks in ClawHub / OpenClaw skills **before installing or trusting them**.

It promotes safer usage, transparency, and awareness when working with third-party skills.

---

## 🔍 What CrawSecure does

- Analyzes skill-related files locally
- Detects potentially dangerous patterns
- Highlights security risks clearly
- Helps users make informed decisions before installation

---

## 🚨 Risk Signals Analyzed

- Dangerous command patterns (e.g. destructive or execution-related behavior)
- References to sensitive files or credentials
- Indicators of unsafe or risky practices

---

## 🔒 Security Philosophy

- Read-only analysis
- No network access
- No code execution
- No file modifications

CrawSecure exists to **increase trust** inside the ClawHub ecosystem.

---

## ⚙️ Execution Model

CrawSecure does **NOT** execute or install any third-party code.

This skill provides a **local CLI tool** that users run manually.

### Using npx (recommended)

```bash
npx crawsecure ./path-to-skill

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
