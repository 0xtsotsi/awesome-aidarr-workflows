# noir-developer

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jp4g/noir-developer/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jp4g/noir-developer/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Develop Noir (.nr) codebases. Use when creating a project or writing code with Noir.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Develop Noir (.nr) codebases. Use when creating a project or writing code with Noir.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run noir-developer`)
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
You are executing the noir-developer workflow. Use the following context:

Description: Develop Noir (.nr) codebases. Use when creating a project or writing code with Noir.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: noir-developer
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Noir Developer

## Workflow

1. Compile (`nargo compile`) Noir program into ACIR.
2. Generate witness (`nargo execute` or NoirJS execute) based on ACIR and user inputs.
3. Prove using ACIR and witness with the selected proving backend.
4. Verify proof with the selected proving backend.

## Task Patterns

### Environment

If the environment is unsupported by `nargo` (e.g. native Windows), guide the user to using GitHub Codespaces (https://noir-lang.org/docs/tooling/devcontainer#using-github-codespaces) or a supported setup (WSL, Docker, or VM).

### Plan

Define private inputs, public inputs (if any), and public outputs (if any) for each Noir program.

### Project Creation

When creating a Noir project, use `nargo new` or `nargo init` to scaffold it.

### Compilation

Use `nargo` (not `noir_wasm`) for compilation; it is the maintained path.

### Validation

Run `nargo test` to validate Noir implementations.

### Proving Backend

Confirm the proving backend choice before implementation details. If the user selects Barretenberg, read `references/barretenberg.md`.

## References

- Run `nargo --help` for the full list of commands.
- Read https://noir-lang.org/docs/ for language syntax, dependencies, and tooling.
- Proving backends:
  - For Barretenberg specifics, read `references/barretenberg.md`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
