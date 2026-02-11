# model-alias-append

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ccapton/model-alias-append/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ccapton/model-alias-append/SKILL.md)
> Category: AI & LLMs

---

## Description

Automatically appends the model alias to the end of every response with integrated hook functionality and configuration change detection.
Use when transparency about which model generated each response is needed.

Use when: providing model transparency, tracking which model generated responses, 
monitoring configuration changes, or ensuring response attribution.


**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.2

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Automatically appends the model alias to the end of every response with integrated hook functionality and configuration change detection.
Use when transparency about which model generated each response is needed.

Use when: providing model transparency, tracking which model generated responses, 
monitoring configuration changes, or ensuring response attribution.


### O - Orchestration
**Trigger:** User-invocable (via `aidarr run model-alias-append`)
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
You are executing the model-alias-append workflow. Use the following context:

Description: Automatically appends the model alias to the end of every response with integrated hook functionality and configuration change detection.
Use when transparency about which model generated each response is needed.

Use when: providing model transparency, tracking which model generated responses, 
monitoring configuration changes, or ensuring response attribution.


Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: model-alias-append
category: AI & LLMs
version: 1.0.2
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Model Alias Append Skill

> Automatically appends model alias to responses with configuration change detection
 
![Model Alias Example](https://github.com/Ccapton/FileRepertory/blob/master/files/model_alias_snapshot.png?raw=true)

## Key Features
- 🔍 **Automatic Detection** - Identifies the model used for each response
- 🏷️ **Alias Appending** - Adds model alias from openclaw config **agents.defaults.models.{yourModelDict}.alias** format like the config below
```
"agents": {
  "defaults": {
    "model": {
      "primary": "gemma3:27b-local",
      "fallbacks": [ "qwen" ]
    },
    "models": {
      "ollama-local/gemma3:27b": {
        "alias": "gemma3:27b-local"
      },
      "qwen-portal/coder-model": {
        "alias": "qwen"
      }
    }
  }
}
```
- 🔄 **Real-time Monitoring** - Watches for configuration changes
- 📢 **Update Notifications** - Shows when config changes occur
- 🛡️ **Format Preservation** - Maintains reply tags and formatting

## Install
```
npx clawhub@latest install model-alias-append
```

## How It Works
1. Intercepts responses before sending
2. Determines which model generated the response  
3. Appends the appropriate model alias
4. Shows update notices when configuration changes

## Setup
> No additional configuration needed - reads from your existing openclaw.json

## Output Example
```
Your response content...

[Model alias configuration updated] // This line will not appear until openclaw.json modified

gemma3:27b-local
```
 
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
