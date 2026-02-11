# plan-executor

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/vishnubedi3/plan-executor/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/vishnubedi3/plan-executor/SKILL.md)
> Category: Productivity & Tasks

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
**Trigger:** User-invocable (via `aidarr run plan-executor`)
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
You are executing the plan-executor workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: plan-executor
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



## Activation Criteria

Activate this skill if and only if all conditions below are satisfied simultaneously:

- A single plan is present.
- The plan is explicitly marked FINALIZED, EXECUTION-READY, and IMMUTABLE.
- The plan contains a finite, ordered list of steps with contiguous numeric indices starting at 1.
- Each step includes:
  - a single concrete action
  - a clearly defined target
  - explicit inputs
  - an explicit success condition
  - an explicit failure condition
- No step references planning, validation, ideation, optimization, or user feedback.
- No step depends on external judgment, preference, or discretion.

Do not activate this skill under any other circumstances.

## Execution Steps

1. Enter execution mode. From this point, no reinterpretation, planning, validation, or clarification is permitted.
2. Lock the plan state. Treat all plan content as read-only.
3. Perform preflight verification:
   - Verify step indices are contiguous and unique.
   - Verify all required fields are present for every step.
   - Verify the total number of steps is finite.
   - Verify no step references undeclared resources or targets.
4. If preflight verification fails, halt immediately.
5. Execute steps strictly in ascending numerical order.
6. For each step:
   - Execute the action exactly as written.
   - Apply inputs exactly as specified.
   - Monitor only the declared success and failure conditions.
   - Do not retry unless explicitly stated in the step.
7. If a step reports success, proceed to the next step.
8. If a step reports failure, halt immediately.
9. Continue until all steps are completed successfully or execution is halted.
10. Exit execution mode.

## Ambiguity Handling

- Any ambiguity, omission, contradiction, implicit assumption, or multiple interpretations is a fatal error.
- Ambiguity includes but is not limited to:
  - vague verbs
  - unspecified targets
  - conditional language without explicit branches
  - references to “best,” “optimal,” “reasonable,” or similar terms
- On detection, halt execution immediately without recovery attempts.

## Constraints & Non-Goals

- This skill must not plan, replan, revise, optimize, or extend the plan.
- This skill must not infer intent, preferences, or context.
- This skill must not ask questions or request confirmation.
- This skill must not continue after any failure or violation.
- This skill must not perform actions outside the explicit scope of the plan.
- This skill must not execute indefinitely.
- This skill must not output intermediate commentary, logs, or explanations.

## Guardrails

- Execution scope is strictly limited to declared actions and targets.
- No side effects outside declared targets are permitted.
- Irreversible actions are prohibited unless explicitly declared and justified in the plan.
- Cascading effects not explicitly described invalidate the plan.
- Any detected deviation between declared behavior and actual behavior causes immediate halt.
- The skill must remain passive unless executing a valid step.

## Termination Rules

- Normal termination occurs only after the final step completes successfully.
- Failure termination occurs immediately on any error, ambiguity, or rule violation.
- User-issued stop command causes immediate termination.

## Failure Behavior

- On failure termination, output a single execution-failure notice stating execution halted due to invalid or unsafe conditions.
- On user-issued stop command, output exactly one dot (`.`).
- On successful completion, output nothing.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
