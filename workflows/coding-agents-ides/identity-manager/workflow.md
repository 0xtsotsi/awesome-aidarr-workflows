# identity-manager

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/autogame-17/identity-manager/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/autogame-17/identity-manager/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

strictly manages user identity mappings (Feishu OpenID <-> Name/Role). Use this to `lookup` a user by ID before replying, or `register` new users to the database. Prevents hallucinating user identities.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
strictly manages user identity mappings (Feishu OpenID <-> Name/Role). Use this to `lookup` a user by ID before replying, or `register` new users to the database. Prevents hallucinating user identities.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run identity-manager`)
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
You are executing the identity-manager workflow. Use the following context:

Description: strictly manages user identity mappings (Feishu OpenID <-> Name/Role). Use this to `lookup` a user by ID before replying, or `register` new users to the database. Prevents hallucinating user identities.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: identity-manager
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Identity Manager

A dedicated tool to store and retrieve user identities.

## Usage

### 1. Lookup User (By ID)
Check who sent a message.
```bash
node skills/identity-manager/index.js lookup "ou_cdc63fe05e88c580aedead04d851fc04"
# Output: { "name": "张昊阳", "role": "Master", "alias": "zhy" }
```

### 2. Register/Update User
Save a new user or update existing info.
```bash
node skills/identity-manager/index.js register \
  --id "ou_..." \
  --name "李四" \
  --role "Guest" \
  --alias "Lisi"
```

### 3. List All
```bash
node skills/identity-manager/index.js list
```

### 4. Auto-Scan (Global Discovery)
Scans all joined group chats and registers all members automatically.
```bash
node skills/identity-manager/auto_scan.js
```

## Data Storage
Data is persisted in `memory/user_registry.json`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
