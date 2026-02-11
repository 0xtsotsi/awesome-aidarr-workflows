# humanize-ai

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/artur-zhdan/humanize-ai/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/artur-zhdan/humanize-ai/SKILL.md)
> Category: AI & LLMs

---

## Description

Humanize AI content by detecting and auto-fixing AI generated content. Humanize AI text using Python scripts. Scans for AI vocabulary, puffery, chatbot artifacts, and auto-replaces filler phrases. Use when you want to analyze text in AI detector and bypass it in future, batch-process files, run automated cleanup, or get a report before manual humanizing.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Humanize AI content by detecting and auto-fixing AI generated content. Humanize AI text using Python scripts. Scans for AI vocabulary, puffery, chatbot artifacts, and auto-replaces filler phrases. Use when you want to analyze text in AI detector and bypass it in future, batch-process files, run automated cleanup, or get a report before manual humanizing.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run humanize-ai`)
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
You are executing the humanize-ai workflow. Use the following context:

Description: Humanize AI content by detecting and auto-fixing AI generated content. Humanize AI text using Python scripts. Scans for AI vocabulary, puffery, chatbot artifacts, and auto-replaces filler phrases. Use when you want to analyze text in AI detector and bypass it in future, batch-process files, run automated cleanup, or get a report before manual humanizing.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: humanize-ai
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Humanize CLI

Command-line tools for detecting and auto-fixing AI writing patterns.

## Scripts

### analyze.py — Detect AI Patterns

Scans text and reports AI vocabulary, puffery, chatbot artifacts, and auto-replaceable phrases.

```bash
# Analyze a file
python scripts/analyze.py input.txt

# Analyze from stdin
echo "This serves as a testament to our commitment" | python scripts/analyze.py

# JSON output for programmatic use
python scripts/analyze.py input.txt --json
```

**Output example:**
```
==================================================
AI PATTERN ANALYSIS - 5 issues found
==================================================

AI VOCABULARY:
  • testament: 1x
  • crucial: 2x

AUTO-REPLACEABLE:
  • "serves as" → "is": 1x
  • "in order to" → "to": 1x
```

---

### humanize.py — Auto-Replace Patterns

Performs automatic replacements for common AI-isms.

```bash
# Humanize and print to stdout
python scripts/humanize.py input.txt

# Write to output file
python scripts/humanize.py input.txt -o output.txt

# Include em dash replacement
python scripts/humanize.py input.txt --fix-dashes

# Quiet mode (no change log)
python scripts/humanize.py input.txt -q
```

**What it fixes automatically:**
- Filler phrases: "in order to" → "to", "due to the fact that" → "because"
- Copula avoidance: "serves as" → "is", "boasts" → "has"
- Sentence starters: removes "Additionally,", "Furthermore,", "Moreover,"
- Curly quotes → straight quotes
- Chatbot artifacts: removes "I hope this helps", "Let me know if", etc.

---

## Workflow

1. **Analyze first** to see what needs fixing:
   ```bash
   python scripts/analyze.py document.txt
   ```

2. **Auto-fix** safe replacements:
   ```bash
   python scripts/humanize.py document.txt -o document_clean.txt
   ```

3. **Manual review** for AI vocabulary and puffery flagged by analyze (these require human judgment)

4. **Re-analyze** to confirm improvements:
   ```bash
   python scripts/analyze.py document_clean.txt
   ```

---

## Customizing Patterns

Edit `scripts/patterns.json` to add/remove:
- `ai_words` — vocabulary that flags but doesn't auto-replace
- `puffery` — promotional language to flag
- `replacements` — phrase → replacement mappings (empty string = delete)
- `chatbot_artifacts` — phrases to auto-remove
- `hedging_phrases` — excessive hedging to flag

---

## Batch Processing

Process multiple files:

```bash
# Analyze all markdown files
for f in *.md; do
  echo "=== $f ===" 
  python scripts/analyze.py "$f"
done

# Humanize all txt files in place
for f in *.txt; do
  python scripts/humanize.py "$f" -o "$f.tmp" && mv "$f.tmp" "$f"
done
```

---

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
