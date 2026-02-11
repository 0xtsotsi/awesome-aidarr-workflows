# java-change-with-tests

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/tanerilyazov/java-change-with-tests/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/tanerilyazov/java-change-with-tests/SKILL.md)
> Category: Coding Agents & IDEs

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
**Trigger:** User-invocable (via `aidarr run java-change-with-tests`)
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
You are executing the java-change-with-tests workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: java-change-with-tests
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# java-change-with-tests

## When to use
- Any Java change that must be merged safely (feature/refactor/bugfix).

## Inputs to request (if missing)
- Acceptance criteria (1-3 bullets).
- Module name (if multi-module repo).
- Build tool and test conventions.
- Whether integration tests are required for the change.

## Steps
1. Repo map (brief): identify the module, entrypoint, and test location.
2. Plan: smallest diff that meets acceptance criteria.
3. Implement: minimal edits.
4. Tests:
   - prefer fast unit tests first
   - add integration tests only when required to validate behavior
5. Verify:
   - run targeted tests
   - run `mvn -q test` (or module-scoped equivalent)
6. Output PR-ready summary with evidence.

## Verification commands (project-specific)
- Use the repo's build tool and record the exact commands and results.
- Prefer targeted unit tests before full test suites.

## Output contract
1) Plan (3-6 steps)
2) Files changed + intent
3) Commands run + results
4) Risks + follow-ups

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
