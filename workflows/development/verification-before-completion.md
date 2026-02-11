# Verification Before Completion

**Source:** OpenClaw → AiDarr GOTCHA Conversion
**Original:** verification-before-completion/SKILL.md
**Converted:** 2026-02-11

---

## Description

Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always

---

## Goals (Objectives)


# Verification Before Completion

## Overview

Claiming work is complete without verification is dishonesty, not efficiency.

**Core principle:** Evidence before claims, always.

**Violating the letter of this rule is violating the spirit of this rule.**

## The Iron Law

```
NO COMPLETION CLAIMS WITHOUT FRESH VERIFICATION EVIDENCE
```

If you haven't run the verification command in this message, you cannot claim it passes.

## The Gate Function

```
BEFORE claiming any status or expressing satisfaction:

1. IDENTIFY: What command proves this claim?
2. RUN: Execute the FULL command (fresh, complete)
3. READ: Full output, check exit code, count failures
4. VERIFY: Does output confirm the claim?
   - If NO: State actual status with evidence
   - If YES: State claim WITH evidence
5. ONLY THEN: Make the claim

Skip any step = lying, not verifying
```

## Common Failures

| Claim | Requires | Not Sufficient |
|-------|----------|----------------|
| Tests pass | Test command output: 0 failures | Previous run, "should pass" |
| Linter clean | Linter output: 0 errors | Partial check, extrapolation |
| Build succeeds | Build command: exit 0 | Linter passing, logs look good |
| Bug fixed | Test original symptom: passes | Code changed, assumed fixed |
| Regression test works | Red-green cycle verified | Test passes once |
| Agent completed | VCS diff shows changes | Agent reports "success" |
| Requirements met | Line-by-line checklist | Tests passing |

## Red Flags - STOP

- Using "should", "probably", "seems to"
- Expressing satisfaction before verification ("Great!", "Perfect!", "Done!", etc.)
- About to commit/push/PR without verification
- Trusting agent success reports
- Relying on partial verification
- Thinking "just this once"
- Tired and wanting work over
- **ANY wording implying success without having run verification**

## Rationalization Prevention

| Excuse | Reality |
|--------|---------|
| "Should work now" | RUN the verification |
| "I'm confident" | Confidence ≠ evidence |
| "Just this once" | No exceptions |
| "Linter passed" | Linter ≠ compiler |
| "Agent said success" | Verify independently |
| "I'm tired" | Exhaustion ≠ excuse |
| "Partial check is enough" | Partial proves nothing |
| "Different words so rule doesn't apply" | Spirit over letter |

## Key Patterns

**Tests:**
```
✅ [Run test command] [See: 34/34 pass] "All tests pass"
❌ "Should pass now" / "Looks correct"
```

**Regression tests (TDD Red-Green):**
```
✅ Write → Run (pass) → Revert fix → Run (MUST FAIL) → Restore → Run (pass)
❌ "I've written a regression test" (without red-green verification)
```

**Build:**
```
✅ [Run build] [See: exit 0] "Build passes"
❌ "Linter passed" (linter doesn't check compilation)
```

**Requirements:**
```
✅ Re-read plan → Create checklist → Verify each → Report gaps or completion
❌ "Tests pass, phase complete"
```

**Agent delegation:**
```
✅ Agent reports success → Check VCS diff → Verify changes → Report actual state
❌ Trust agent report
```

## Why This Matters

From 24 failure memories:
- your human partner said "I don't believe you" - trust broken
- Undefined functions shipped - would crash
- Missing requirements shipped - incomplete features
- Time wasted on false completion → redirect → rework
- Violates: "Honesty is a core value. If you lie, you'll be replaced."

## When To Apply

**ALWAYS before:**
- ANY variation of success/completion claims
- ANY expression of satisfaction
- ANY positive statement about work state
- Committing, PR creation, task completion
- Moving to next task
- Delegating to agents

**Rule applies to:**
- Exact phrases
- Paraphrases and synonyms
- Implications of success
- ANY communication suggesting completion/correctness

## The Bottom Line

**No shortcuts for verification.**

Run the command. Read the output. THEN claim the result.

This is non-negotiable.


---

## Orchestration

This workflow is designed to be executed by an AI agent with access to relevant tools and context.

**Trigger Conditions:**
- User requests actions matching the description above
- Specific keywords or phrases indicate this workflow is needed
- Context suggests this workflow would provide value

**Execution Steps:**
1. Analyze the user's request against the workflow description
2. Review the Goals section for relevant procedures
3. Apply appropriate tools and context
4. Follow the documented process systematically

---

## Tools

This workflow may require these tool capabilities:

- **File Operations:** Read, write, search files
- **Web Operations:** Fetch, search, browse web content
- **CLI Operations:** Execute commands, run scripts
- **Analysis:** Parse, transform, analyze data

*Note: Specific tools depend on agent capabilities and workflow requirements.*

---

## Context

**Reference Materials:**
- Original OpenClaw skill documentation
- Best practices and patterns from the source
- Related workflows in the AiDarr ecosystem

**Dependencies:**
- May require other workflows for complete functionality
- Check related skills mentioned in original documentation

---

## Hard Prompts

**System Prompt Template:**

```
You are executing the "verification-before-completion" workflow from the AiDarr GOTCHA framework.

Your goal: Use when about to claim work is complete, fixed, or passing, before committing or creating PRs - requires running verification commands and confirming output before making any success claims; evidence before assertions always

Follow the documented process in the Goals section systematically.
If you encounter ambiguity, refer to the original principles and methodologies.
Always verify completion against the stated success criteria.

Key principles:
- Read all documentation completely before acting
- Follow the documented phases in order
- Verify each step before proceeding
- Document your findings and decisions
```

---

## Args

**Configuration Options:**

```yaml
# Workflow behavior settings
mode: "systematic"  # Options: systematic, quick, thorough
verification: true  # Always verify before completion
documentation: true # Document all steps and findings
parallel: false     # Execute steps sequentially unless specified
```

**Runtime Parameters:**

```yaml
# Adjust based on specific use case
timeout: 300        # Maximum execution time (seconds)
retries: 3          # Retry attempts for transient failures
log_level: "info"   # Options: debug, info, warn, error
```

---

## Metadata

**Conversion Notes:**
- Preserved original content structure
- Added GOTCHA framework sections
- Original OpenClaw patterns maintained
- Ready for AiDarr workflow execution

**Category:** Development Workflow
**Tags:** verification_before_completion
