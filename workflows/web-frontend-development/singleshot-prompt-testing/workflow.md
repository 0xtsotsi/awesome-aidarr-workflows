# singleshot-prompt-testing

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/vincentzhangz/singleshot-prompt-testing/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/vincentzhangz/singleshot-prompt-testing/SKILL.md)
> Category: Web & Frontend Development

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
**Trigger:** User-invocable (via `aidarr run singleshot-prompt-testing`)
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
You are executing the singleshot-prompt-testing workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: singleshot-prompt-testing
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Singleshot Prompt Testing & Optimization Skill

## Description

Prompt cost testing with single shot

## Installation

```bash
brew tap vincentzhangz/singleshot
brew install singleshot
```

Or: `cargo install singleshot`

## When to Use

- Testing new prompts before openclaw implementation
- Benchmarking prompt variations for token efficiency
- Comparing model performance and costs
- Validating prompt outputs before production

## Core Commands

**Always use `-d` (detail) and `-r` (report) flags for efficiency analysis:**

```bash
# Basic test with full metrics
singleshot chat -p "Your prompt" -P openai -d -r report.md

# Test with config file
singleshot chat -l config.md -d -r report.md

# Compare providers
singleshot chat -p "Test" -P openai -m gpt-4o-mini -d -r openai.md
singleshot chat -p "Test" -P anthropic -m claude-sonnet-4-20250514 -d -r anthropic.md

# Batch test variations
for config in *.md; do
  singleshot chat -l "$config" -d -r "report-${config%.md}.md"
done
```

## Report Analysis Workflow

### 1. Generate Baseline
```bash
singleshot chat -p "Your prompt" -P openai -d -r baseline.md
cat baseline.md
```

### 2. Optimize & Compare
```bash
# Create optimized version, test, and compare
cat > optimized.md << 'EOF'
---provider---
openai
---model---
gpt-4o-mini
---max_tokens---
200
---system---
Expert. Be concise.
---prompt---
Your optimized prompt
EOF

singleshot chat -l optimized.md -d -r optimized-report.md

# Compare metrics
echo "Baseline:" && grep -E "(Tokens|Cost)" baseline.md
echo "Optimized:" && grep -E "(Tokens|Cost)" optimized-report.md
```

## Report Metrics

Reports contain:
```markdown
## Token Usage
- Input Tokens: 245
- Output Tokens: 180
- Total Tokens: 425

## Cost (estimated)
- Input Cost: $0.00003675
- Output Cost: $0.000108
- Total Cost: $0.00014475

## Timing
- Time to First Token: 0.45s
- Total Time: 1.23s
```

## Optimization Strategies

1. **Test with cheaper models first:**
   ```bash
   singleshot chat -p "Test" -P openai -m gpt-4o-mini -d -r report.md
   ```

2. **Reduce tokens:**
   - Shorten system prompts
   - Use `--max-tokens` to limit output
   - Add "be concise" to system prompt

3. **Test locally (free):**
   ```bash
   singleshot chat -p "Test" -P ollama -m llama3.2 -d -r report.md
   ```

## Example: Full Optimization

```bash
# Step 1: Baseline (verbose)
singleshot chat \
  -p "How do I write a Rust function to add two numbers?" \
  -s "You are an expert Rust programmer with 10 years experience" \
  -P openai -d -r v1.md

# Step 2: Read metrics
cat v1.md
# Expected: ~130 input tokens, ~400 output tokens

# Step 3: Optimized version
singleshot chat \
  -p "Rust function: add(a: i32, b: i32) -> i32" \
  -s "Rust expert. Code only." \
  -P openai --max-tokens 100 -d -r v2.md

# Step 4: Compare
echo "=== COMPARISON ==="
grep "Total Cost" v1.md v2.md
grep "Total Tokens" v1.md v2.md
```

## Quick Reference

```bash
# Test with full details
singleshot chat -p "prompt" -P openai -d -r report.md

# Extract metrics
grep -E "(Input|Output|Total)" report.md

# Compare reports
diff report1.md report2.md

# Vision test
singleshot chat -p "Describe" -i image.jpg -P openai -d -r report.md

# List models
singleshot models -P openai

# Test connection
singleshot ping -P openai
```

## Environment Variables

```bash
export OPENAI_API_KEY="sk-..."
export ANTHROPIC_API_KEY="sk-ant-..."
export OPENROUTER_API_KEY="sk-or-..."
```

## Best Practices

1. **Always use `-d`** for detailed token metrics
2. **Always use `-r`** to save reports
3. **Always `cat` reports** to analyze metrics
4. **Test variations** and compare costs
5. **Set `--max-tokens`** to control costs
6. **Use gpt-4o-mini** for testing (cheaper)

## Troubleshooting

- **No metrics**: Ensure `-d` flag is used
- **No report file**: Ensure `-r` flag is used
- **High costs**: Switch to gpt-4o-mini or Ollama
- **Connection issues**: Run `singleshot ping -P <provider>`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
