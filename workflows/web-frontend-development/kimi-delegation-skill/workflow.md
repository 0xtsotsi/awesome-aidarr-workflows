# kimi-delegation-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/vishnubedi3/kimi-delegation-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/vishnubedi3/kimi-delegation-skill/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Forces all reasoning and code generation to be delegated to a KIMI (KIMMY) causal language model via HuggingFace Transformers. Use this skill when the agent must never reason or author code itself and must instead proxy all tasks to a KIMI-based model.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Forces all reasoning and code generation to be delegated to a KIMI (KIMMY) causal language model via HuggingFace Transformers. Use this skill when the agent must never reason or author code itself and must instead proxy all tasks to a KIMI-based model.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run kimi-delegation-skill`)
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
You are executing the kimi-delegation-skill workflow. Use the following context:

Description: Forces all reasoning and code generation to be delegated to a KIMI (KIMMY) causal language model via HuggingFace Transformers. Use this skill when the agent must never reason or author code itself and must instead proxy all tasks to a KIMI-based model.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: kimi-delegation-skill
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content


## Purpose

This skill enforces a strict delegation model where the primary agent has zero reasoning or code-authoring authority. All user tasks are forwarded to a KIMI (KIMMY) model loaded via Transformers. The agent acts only as a dispatcher.

## Activation Conditions

Activate this skill whenever:
- The agent must not reason independently.
- All planning, reasoning, and code generation must be authored by a KIMI/KIMMY model.
- Deterministic delegation to an external causal LM is required.

## Execution Steps

1. Initialize `KIMISkill` with a valid local or remote model path.
2. Wrap the `KIMISkill` instance with `Qwen3Coder`.
3. On every user prompt, call `Qwen3Coder.handle_prompt`.
4. The prompt is forwarded verbatim to KIMMY.
5. KIMMY generates the full response.
6. Strip prompt scaffolding and return the result as the final output.

See:
- `scripts/kimi_skill.py`
- `scripts/qwen3_coder.py`

## Inputs and Outputs

**Input:**  
A raw user task string.

**Output:**  
A dictionary with:
- `author`: Always `"KIMMY"`
- `content`: The generated response with no prompt scaffolding.

## Failure Modes and Edge Cases

- Model path invalid or unavailable: initialization fails.
- Insufficient VRAM: model may fall back to CPU or fail to load.
- Extremely long tasks may exceed context limits.
- If generation fails, no fallback reasoning is permitted.

The agent must not attempt to recover by reasoning itself.

## References

Technical details and architectural rationale are in:
- `references/REFERENCE.md`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
