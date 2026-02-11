# agentlens

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/nguyenphutrong/agentlens/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/nguyenphutrong/agentlens/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Navigate and understand codebases using agentlens hierarchical documentation. Use when exploring new projects, finding modules, locating symbols in large files, finding TODOs/warnings, or understanding code structure.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Navigate and understand codebases using agentlens hierarchical documentation. Use when exploring new projects, finding modules, locating symbols in large files, finding TODOs/warnings, or understanding code structure.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run agentlens`)
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
You are executing the agentlens workflow. Use the following context:

Description: Navigate and understand codebases using agentlens hierarchical documentation. Use when exploring new projects, finding modules, locating symbols in large files, finding TODOs/warnings, or understanding code structure.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: agentlens
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# AgentLens - Codebase Navigation

## Before Working on Any Codebase
Always start by reading `.agentlens/INDEX.md` for the project map.

## Navigation Hierarchy

| Level | File | Purpose |
|-------|------|---------|
| L0 | `INDEX.md` | Project overview, all modules listed |
| L1 | `modules/{slug}/MODULE.md` | Module details, file list |
| L1 | `modules/{slug}/outline.md` | Symbols in large files |
| L1 | `modules/{slug}/memory.md` | TODOs, warnings, business rules |
| L1 | `modules/{slug}/imports.md` | File dependencies |
| L2 | `files/{slug}.md` | Deep docs for complex files |

## Navigation Flow

```
INDEX.md → Find module → MODULE.md → outline.md/memory.md → Source file
```

## When To Read What

| You Need | Read This |
|----------|-----------|
| Project overview | `.agentlens/INDEX.md` |
| Find a module | INDEX.md, search module name |
| Understand a module | `modules/{slug}/MODULE.md` |
| Find function/class in large file | `modules/{slug}/outline.md` |
| Find TODOs, warnings, rules | `modules/{slug}/memory.md` |
| Understand file dependencies | `modules/{slug}/imports.md` |

## Best Practices

1. **Don't read source files directly** for large codebases - use outline.md first
2. **Check memory.md before modifying** code to see warnings and TODOs
3. **Use outline.md to locate symbols**, then read only the needed source sections
4. **Regenerate docs** with `agentlens` command if they seem stale

For detailed navigation patterns, see [references/navigation.md](references/navigation.md)
For structure explanation, see [references/structure.md](references/structure.md)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
