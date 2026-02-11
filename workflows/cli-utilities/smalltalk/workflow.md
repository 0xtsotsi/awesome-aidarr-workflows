# smalltalk

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/johnmci/smalltalk/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/johnmci/smalltalk/SKILL.md)
> Category: CLI Utilities

---

## Description

Interact with live Smalltalk image (Cuis or Squeak). Use for evaluating Smalltalk code, browsing classes, viewing method source, defining classes/methods, querying hierarchy and categories.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Interact with live Smalltalk image (Cuis or Squeak). Use for evaluating Smalltalk code, browsing classes, viewing method source, defining classes/methods, querying hierarchy and categories.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run smalltalk`)
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
You are executing the smalltalk workflow. Use the following context:

Description: Interact with live Smalltalk image (Cuis or Squeak). Use for evaluating Smalltalk code, browsing classes, viewing method source, defining classes/methods, querying hierarchy and categories.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: smalltalk
category: CLI Utilities
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Smalltalk Skill

Execute Smalltalk code and browse live Squeak/Cuis images via MCP.

## Prerequisites

**Get the ClaudeSmalltalk repo first:**

```bash
git clone https://github.com/CorporateSmalltalkConsultingLtd/ClaudeSmalltalk.git
```

This repo contains:
- MCP server code for Squeak (`MCP-Server-Squeak.st`)
- Setup documentation (`SQUEAK-SETUP.md`, `CLAWDBOT-SETUP.md`)
- This Clawdbot skill (`clawdbot/`)

## Setup

1. **Set up Squeak with MCP server** — see [SQUEAK-SETUP.md](https://github.com/CorporateSmalltalkConsultingLtd/ClaudeSmalltalk/blob/main/SQUEAK-SETUP.md)
2. **Configure Clawdbot** — see [CLAWDBOT-SETUP.md](https://github.com/CorporateSmalltalkConsultingLtd/ClaudeSmalltalk/blob/main/CLAWDBOT-SETUP.md)

## Usage

```bash
# Check setup
python3 smalltalk.py --check

# Evaluate code
python3 smalltalk.py evaluate "3 factorial"
python3 smalltalk.py evaluate "Date today"

# Browse a class
python3 smalltalk.py browse OrderedCollection

# View method source
python3 smalltalk.py method-source String asUppercase

# List classes (with optional prefix filter)
python3 smalltalk.py list-classes Collection

# Get class hierarchy
python3 smalltalk.py hierarchy OrderedCollection

# Get subclasses  
python3 smalltalk.py subclasses Collection

# List all categories
python3 smalltalk.py list-categories

# List classes in a category
python3 smalltalk.py classes-in-category "Collections-Sequenceable"

# Define a new class
python3 smalltalk.py define-class "Object subclass: #Counter instanceVariableNames: 'count' classVariableNames: '' poolDictionaries: '' category: 'MyApp'"

# Define a method
python3 smalltalk.py define-method Counter "increment
    count := (count ifNil: [0]) + 1.
    ^ count"

# Delete a method
python3 smalltalk.py delete-method Counter increment

# Delete a class
python3 smalltalk.py delete-class Counter
```

## Commands

| Command | Description |
|---------|-------------|
| `--check` | Verify VM/image paths and dependencies |
| `--debug` | Debug hung system (sends SIGUSR1, captures stack trace) |
| `evaluate <code>` | Execute Smalltalk code, return result |
| `browse <class>` | Get class metadata (superclass, ivars, methods) |
| `method-source <class> <selector>` | View method source code |
| `define-class <definition>` | Create or modify a class |
| `define-method <class> <source>` | Add or update a method |
| `delete-method <class> <selector>` | Remove a method |
| `delete-class <class>` | Remove a class |
| `list-classes [prefix]` | List classes, optionally filtered |
| `hierarchy <class>` | Get superclass chain |
| `subclasses <class>` | Get immediate subclasses |
| `list-categories` | List all system categories |
| `classes-in-category <cat>` | List classes in a category |

## Environment Variables

| Variable | Description |
|----------|-------------|
| `SQUEAK_VM_PATH` | Path to Squeak/Cuis VM executable |
| `SQUEAK_IMAGE_PATH` | Path to Smalltalk image with MCP server |

## Notes

- Requires xvfb for headless operation on Linux servers
- Uses Squeak 6.0 MCP server (GUI stays responsive if display available)
- `saveImage` intentionally excluded for safety

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
