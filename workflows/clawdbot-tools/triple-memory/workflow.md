# triple-memory

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ktpriyatham/triple-memory/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ktpriyatham/triple-memory/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Complete memory system combining LanceDB auto-recall, Git-Notes structured memory, and file-based workspace search. Use when setting up comprehensive agent memory, when you need persistent context across sessions, or when managing decisions/preferences/tasks with multiple memory backends working together.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Complete memory system combining LanceDB auto-recall, Git-Notes structured memory, and file-based workspace search. Use when setting up comprehensive agent memory, when you need persistent context across sessions, or when managing decisions/preferences/tasks with multiple memory backends working together.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run triple-memory`)
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
You are executing the triple-memory workflow. Use the following context:

Description: Complete memory system combining LanceDB auto-recall, Git-Notes structured memory, and file-based workspace search. Use when setting up comprehensive agent memory, when you need persistent context across sessions, or when managing decisions/preferences/tasks with multiple memory backends working together.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: triple-memory
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Triple Memory System

A comprehensive memory architecture combining three complementary systems for maximum context retention across sessions.

## Architecture Overview

```
User Message
     ↓
[LanceDB auto-recall] → injects relevant conversation memories
     ↓
Agent responds (using all 3 systems)
     ↓
[LanceDB auto-capture] → stores preferences/decisions automatically
     ↓
[Git-Notes] → structured decisions with entity extraction
     ↓
[File updates] → persistent workspace docs
```

## The Three Systems

### 1. LanceDB (Conversation Memory)
- **Auto-recall:** Relevant memories injected before each response
- **Auto-capture:** Preferences/decisions/facts stored automatically
- **Tools:** `memory_recall`, `memory_store`, `memory_forget`
- **Triggers:** "remember", "prefer", "my X is", "I like/hate/want"

### 2. Git-Notes Memory (Structured, Local)
- **Branch-aware:** Memories isolated per git branch
- **Entity extraction:** Auto-extracts topics, names, concepts
- **Importance levels:** critical, high, normal, low
- **No external API calls**

### 3. File Search (Workspace)
- **Searches:** MEMORY.md, memory/*.md, any workspace file
- **Script:** `scripts/file-search.sh`

## Setup

### Enable LanceDB Plugin
```json
{
  "plugins": {
    "slots": { "memory": "memory-lancedb" },
    "entries": {
      "memory-lancedb": {
        "enabled": true,
        "config": {
          "embedding": { "apiKey": "${OPENAI_API_KEY}", "model": "text-embedding-3-small" },
          "autoRecall": true,
          "autoCapture": true
        }
      }
    }
  }
}
```

### Install Git-Notes Memory
```bash
clawdhub install git-notes-memory
```

### Create File Search Script
Copy `scripts/file-search.sh` to your workspace.

## Usage

### Session Start (Always)
```bash
python3 skills/git-notes-memory/memory.py -p $WORKSPACE sync --start
```

### Store Important Decisions
```bash
python3 skills/git-notes-memory/memory.py -p $WORKSPACE remember \
  '{"decision": "Use PostgreSQL", "reason": "Team expertise"}' \
  -t architecture,database -i h
```

### Search Workspace Files
```bash
./scripts/file-search.sh "database config" 5
```

### Conversation Memory (Automatic)
LanceDB handles this automatically. Manual tools:
- `memory_recall "query"` - search conversation memory
- `memory_store "text"` - manually store something
- `memory_forget` - delete memories (GDPR)

## Importance Levels

| Flag | Level | When to Use |
|------|-------|-------------|
| `-i c` | Critical | "always remember", explicit preferences |
| `-i h` | High | Decisions, corrections, preferences |
| `-i n` | Normal | General information |
| `-i l` | Low | Temporary notes |

## When to Use Each System

| System | Use For |
|--------|---------|
| **LanceDB** | Conversation context, auto-retrieval |
| **Git-Notes** | Structured decisions, searchable by entity/tag |
| **File Search** | Workspace docs, daily logs, MEMORY.md |

## File Structure

```
workspace/
├── MEMORY.md              # Long-term curated memory
├── memory/
│   ├── active-context.md  # Current session state
│   └── YYYY-MM-DD.md      # Daily logs
├── scripts/
│   └── file-search.sh     # Workspace search
└── skills/
    └── git-notes-memory/  # Structured memory
```

## Silent Operation

Never announce memory operations to users. Just do it:
- ❌ "I'll remember this"
- ❌ "Saving to memory"
- ✅ (silently store and continue)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
