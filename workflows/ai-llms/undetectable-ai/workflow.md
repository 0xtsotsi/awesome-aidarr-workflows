# undetectable-ai

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/artur-zhdan/undetectable-ai/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/artur-zhdan/undetectable-ai/SKILL.md)
> Category: AI & LLMs

---

## Description

Make AI text undetectable. TypeScript CLI that scans ChatGPT, Claude, OpenClaw output for patterns flagged by GPTZero, Turnitin, Originality.ai, then auto-fixes them to pass as human-written. Use to bypass AI detection, evade checkers, or humanize text before submission.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Make AI text undetectable. TypeScript CLI that scans ChatGPT, Claude, OpenClaw output for patterns flagged by GPTZero, Turnitin, Originality.ai, then auto-fixes them to pass as human-written. Use to bypass AI detection, evade checkers, or humanize text before submission.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run undetectable-ai`)
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
You are executing the undetectable-ai workflow. Use the following context:

Description: Make AI text undetectable. TypeScript CLI that scans ChatGPT, Claude, OpenClaw output for patterns flagged by GPTZero, Turnitin, Originality.ai, then auto-fixes them to pass as human-written. Use to bypass AI detection, evade checkers, or humanize text before submission.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: undetectable-ai
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Undetectable AI

TypeScript CLI tools for bypassing AI content detectors by removing telltale patterns.

## Setup

```bash
cd scripts && npm install
```

## Scripts

### analyze.ts — Scan for Detectable Patterns

Finds patterns that AI detectors look for: vocabulary, sentence structure, artifacts.

```bash
# Analyze a file
npx ts-node scripts/analyze.ts input.txt

# From stdin
echo "This serves as a testament" | npx ts-node scripts/analyze.ts

# JSON output
npx ts-node scripts/analyze.ts input.txt --json
```

**Output:**
```
==================================================
AI DETECTION SCAN - 5 issues found
==================================================

AI VOCABULARY:
  • testament: 1x
  • crucial: 2x

AUTO-FIXABLE:
  • "serves as" → "is": 1x
```

---

### transform.ts — Auto-Fix Patterns

Rewrites text to evade detection.

```bash
# Transform and print
npx ts-node scripts/transform.ts input.txt

# Write to file
npx ts-node scripts/transform.ts input.txt -o output.txt

# Fix em dashes too
npx ts-node scripts/transform.ts input.txt --fix-dashes

# Quiet mode
npx ts-node scripts/transform.ts input.txt -q
```

**What it fixes:**
- Filler phrases: "in order to" → "to"
- AI vocabulary: "utilize" → "use", "leverage" → "use"
- Sentence starters: removes "Additionally,", "Furthermore,"
- Chatbot artifacts: removes entire sentences with "I hope this helps", etc.
- Curly quotes → straight quotes
- Capitalization after removals

---

## Workflow

1. **Scan** to see detection risk:
   ```bash
   npx ts-node scripts/analyze.ts essay.txt
   ```

2. **Auto-fix** mechanical patterns:
   ```bash
   npx ts-node scripts/transform.ts essay.txt -o essay_clean.txt
   ```

3. **Manual pass** for flagged AI vocabulary (requires judgment)

4. **Re-scan** to verify:
   ```bash
   npx ts-node scripts/analyze.ts essay_clean.txt
   ```

---

## Customizing

Edit `scripts/patterns.json`:
- `ai_words` — vocabulary to flag (manual fix needed)
- `puffery` — promotional language to flag
- `replacements` — auto-replace mappings
- `chatbot_artifacts` — phrases that trigger full sentence removal

---

## Batch Processing

```bash
# Scan all docs
for f in *.txt; do
  echo "=== $f ==="
  npx ts-node scripts/analyze.ts "$f"
done

# Transform all
for f in *.md; do
  npx ts-node scripts/transform.ts "$f" -o "${f%.md}_clean.md" -q
done
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
