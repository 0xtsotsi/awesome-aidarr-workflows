# model-usage

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/model-usage/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/model-usage/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Use CodexBar CLI local cost usage to summarize per-model usage for Codex or Claude, including the current (most recent) model or a full model breakdown. Trigger when asked for model-level usage/cost data from codexbar, or when you need a scriptable per-model summary from codexbar cost JSON.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Use CodexBar CLI local cost usage to summarize per-model usage for Codex or Claude, including the current (most recent) model or a full model breakdown. Trigger when asked for model-level usage/cost data from codexbar, or when you need a scriptable per-model summary from codexbar cost JSON.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run model-usage`)
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
You are executing the model-usage workflow. Use the following context:

Description: Use CodexBar CLI local cost usage to summarize per-model usage for Codex or Claude, including the current (most recent) model or a full model breakdown. Trigger when asked for model-level usage/cost data from codexbar, or when you need a scriptable per-model summary from codexbar cost JSON.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: model-usage
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Model usage

## Overview
Get per-model usage cost from CodexBar's local cost logs. Supports "current model" (most recent daily entry) or "all models" summaries for Codex or Claude.

TODO: add Linux CLI support guidance once CodexBar CLI install path is documented for Linux.

## Quick start
1) Fetch cost JSON via CodexBar CLI or pass a JSON file.
2) Use the bundled script to summarize by model.

```bash
python {baseDir}/scripts/model_usage.py --provider codex --mode current
python {baseDir}/scripts/model_usage.py --provider codex --mode all
python {baseDir}/scripts/model_usage.py --provider claude --mode all --format json --pretty
```

## Current model logic
- Uses the most recent daily row with `modelBreakdowns`.
- Picks the model with the highest cost in that row.
- Falls back to the last entry in `modelsUsed` when breakdowns are missing.
- Override with `--model <name>` when you need a specific model.

## Inputs
- Default: runs `codexbar cost --format json --provider <codex|claude>`.
- File or stdin:

```bash
codexbar cost --provider codex --format json > /tmp/cost.json
python {baseDir}/scripts/model_usage.py --input /tmp/cost.json --mode all
cat /tmp/cost.json | python {baseDir}/scripts/model_usage.py --input - --mode current
```

## Output
- Text (default) or JSON (`--format json --pretty`).
- Values are cost-only per model; tokens are not split by model in CodexBar output.

## References
- Read `references/codexbar-cli.md` for CLI flags and cost JSON fields.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
