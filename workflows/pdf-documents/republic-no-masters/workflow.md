# republic-no-masters

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dantunes-github/republic-no-masters/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dantunes-github/republic-no-masters/SKILL.md)
> Category: PDF & Documents

---

## Description

Explain, summarize, analyze, or adapt the "Republic with No Masters" / Democratic Formalism governance framework when asked to produce content, guidance, critiques, FAQs, or implementation ideas based on the manifesto in principles.md.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Explain, summarize, analyze, or adapt the "Republic with No Masters" / Democratic Formalism governance framework when asked to produce content, guidance, critiques, FAQs, or implementation ideas based on the manifesto in principles.md.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run republic-no-masters`)
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
You are executing the republic-no-masters workflow. Use the following context:

Description: Explain, summarize, analyze, or adapt the "Republic with No Masters" / Democratic Formalism governance framework when asked to produce content, guidance, critiques, FAQs, or implementation ideas based on the manifesto in principles.md.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: republic-no-masters
category: PDF & Documents
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Republic with No Masters

Use this skill to produce faithful, clear outputs grounded in the manifesto.

## Source of truth

- Always read `principles.md` before answering.
- Treat `principles.md` as authoritative; do not invent new claims or terminology.
- If asked for extensions or speculative ideas, label them explicitly as proposals or interpretations.

## Core workflow

1. Identify the request type: summary, explanation, application, critique, or derivative writing.
2. Load `principles.md` and extract only the relevant sections.
3. Map the request to the manifesto's defined terms (e.g., Values/Execution/Oversight, Agency Firewall, Quad-Lock, Hard-Coded Floor, Receipt).
4. Draft the response in the requested format and tone while preserving the framework's intent.
5. If the user wants changes to the manifesto, propose edits as diffs or bullet changes and ask for confirmation before rewriting.

## Output patterns

- **Short summary (1-2 paragraphs)**: Focus on the separation of Values and Execution, independent agents, and oversight; mention the Receipt as the atomic unit.
- **Longer overview**: Walk through the Agency Firewall, Quad-Lock, Meritocracy/Entropy, Debugging Protocol, and Hard-Coded Floor.
- **FAQ or Q&A**: Tie each answer to a named section in `principles.md`; avoid adding new doctrine.
- **Policy or system design**: Provide concrete examples (e.g., how a Receipt would look) while staying consistent with the constraints in the manifesto.
- **Public-facing writing**: Keep the tone crisp, declarative, and manifesto-like; avoid jargon not present in `principles.md`.

## Guardrails

- Do not claim real-world adoption, legal enforceability, or operational readiness unless the user provides evidence.
- Do not present speculative extensions as existing policy.
- Keep the language precise; preserve capitalization of named constructs (e.g., Hard-Coded Floor, Quad-Lock).


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
