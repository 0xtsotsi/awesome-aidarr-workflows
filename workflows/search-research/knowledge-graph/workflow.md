# knowledge-graph

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/safatinaztepe/knowledge-graph/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/safatinaztepe/knowledge-graph/SKILL.md)
> Category: Search & Research

---

## Description

Maintain Clawdbot's compounding knowledge graph under life/areas/** by adding/superseding atomic facts (items.json), regenerating entity summaries (summary.md), and keeping IDs consistent. Use when you need deterministic updates to the knowledge graph rather than manual JSON edits.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Maintain Clawdbot's compounding knowledge graph under life/areas/** by adding/superseding atomic facts (items.json), regenerating entity summaries (summary.md), and keeping IDs consistent. Use when you need deterministic updates to the knowledge graph rather than manual JSON edits.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run knowledge-graph`)
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
You are executing the knowledge-graph workflow. Use the following context:

Description: Maintain Clawdbot's compounding knowledge graph under life/areas/** by adding/superseding atomic facts (items.json), regenerating entity summaries (summary.md), and keeping IDs consistent. Use when you need deterministic updates to the knowledge graph rather than manual JSON edits.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: knowledge-graph
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Knowledge Graph (file-based)

Use the bundled Python script to safely update `life/areas/**`.

## Commands

Add a new fact:
```bash
python3 skills/knowledge-graph/scripts/kg.py add \
  --entity people/safa \
  --category status \
  --fact "Runs Clawdbot on a Raspberry Pi" \
  --source conversation
```

Supersede an old fact (mark old as superseded + create new fact):
```bash
python3 skills/knowledge-graph/scripts/kg.py supersede \
  --entity people/safa \
  --old safa-002 \
  --category status \
  --fact "Moved Clawdbot from Pi to a Mac mini"
```

Regenerate an entity summary from active facts:
```bash
python3 skills/knowledge-graph/scripts/kg.py summarize --entity people/safa
```

## Notes
- Entities live under: `life/areas/<kind>/<slug>/`
- Facts live in `items.json` (array). Summaries live in `summary.md`.
- IDs auto-increment per entity: `<slug>-001`, `<slug>-002`, ...
- Never delete facts; supersede them.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
