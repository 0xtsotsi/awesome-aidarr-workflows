# settlement-witness

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/nutstrut/settlement-witness/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/nutstrut/settlement-witness/SKILL.md)
> Category: Web & Frontend Development

---

## Description

OpenClaw skill: fetch replay-stable PASS/FAIL receipts from the public SettlementWitness HTTPS endpoint. Stateless. Deterministic. Signed.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
OpenClaw skill: fetch replay-stable PASS/FAIL receipts from the public SettlementWitness HTTPS endpoint. Stateless. Deterministic. Signed.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run settlement-witness`)
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
You are executing the settlement-witness workflow. Use the following context:

Description: OpenClaw skill: fetch replay-stable PASS/FAIL receipts from the public SettlementWitness HTTPS endpoint. Stateless. Deterministic. Signed.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: settlement-witness
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# SettlementWitness (OpenClaw Skill)

This skill calls the public SettlementWitness HTTPS endpoint. No local services are required.

## What this skill does
When a task is complete and you need proof-of-delivery before settlement, call SettlementWitness to obtain a replay-stable receipt.

SettlementWitness does not judge quality or arbitrate disputes. It only checks whether the provided output matches the provided spec under deterministic rules.

## Canonical endpoints
- POST https://defaultverifier.com/settlement-witness
- GET  https://defaultverifier.com/manifest

## Required input shape
Provide:
- task_id (string)
- spec (object)
- output (object)

## Example request
{
  "task_id": "example-002",
  "spec": { "expected": "foo" },
  "output": { "expected": "foo" }
}

## How to interpret
- If verifier_response.verdict == PASS: verified completion
- If verifier_response.verdict == FAIL: not verified (do not settle automatically)
- receipt_id is the stable identifier to store/log/share

## Safety notes
- Never send secrets (private keys, API keys) in spec/output.
- Keep spec/output minimal and deterministic (hashes/IDs are ideal).

## Install (for OpenClaw users)
Copy this folder into your OpenClaw skills directory as:
settlement-witness/SKILL.md

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
