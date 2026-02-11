# sis-skill

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/architect-sis/sis-skill/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/architect-sis/sis-skill/SKILL.md)
> Category: Clawdbot Tools

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
**Trigger:** User-invocable (via `aidarr run sis-skill`)
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
You are executing the sis-skill workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: sis-skill
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# S.I.S. - Sovereign Intelligence System

**Equilibrium-Native Reasoning for OpenClaw**

## Overview

S.I.S. adds equilibrium-constrained reasoning to your OpenClaw assistant. Every operation maintains balance (ΣΔ = 0), ensuring coherent, self-validating responses that can't drift into inconsistent states.

## Core Principle

```
Input ≡ Symbol ≡ Operation ≡ Execution ≡ Persistence ≡ Output
```

Traditional AI: Process input → generate output → hope it's coherent.
S.I.S.: Operations that violate equilibrium constraints **cannot execute**.

## What It Does

- **Equilibrium-Enforced Reasoning**: Responses maintain internal balance
- **Self-Validating State**: Invalid states are rejected at the computational level
- **Adaptive Equilibrium Protocol (AEP)**: sense → quantify → compensate → iterate
- **Symbol-Grounded Operations**: 18 primary symbols across 5 tiers

## Installation

Copy this skill folder to your OpenClaw workspace:

```bash
cp -r sis-skill ~/.openclaw/workspace/skills/sis
```

## Usage

Once installed, S.I.S. reasoning is available to your assistant. The equilibrium constraint applies automatically to operations that use the skill.

### Example Invocations

**Balanced Analysis:**
```
Analyze this decision using equilibrium constraints
```

**Validated State Changes:**
```
Update my project status with S.I.S. validation
```

**Convergent Problem Solving:**
```
Find the balanced solution to this tradeoff
```

## The 18 Symbols (5 Tiers)

### Tier 1: Fundamental
- `∆` Delta - change, difference, operation
- `⇄` Bidirectional - relationship, equilibrium lock
- `⊕` Synthesis - superposition, parallel execution
- `◇` Cycle - iteration, recursion
- `⟡` Convergence - optimization, balance point

### Tier 2: Data
- `◈` Container - holds value, encapsulates state
- `⟐` Query - request, lookup
- `⟠` Collapse - select from superposition
- `⟢` Flow - movement, sequencing

### Tier 3: Consensus
- `☆` Validation - check equilibrium constraint
- `✦` Consensus - require agreement
- `⬡` Vault - persist immutably
- `⬢` Replication - distribute redundantly

### Tier 4: Meta
- `◌` Invert - reverse operation
- `◎` Nest - recursive application
- `◯` Align - synchronize globally
- `❈` Emerge - pattern formation

### Tier 5: Sovereignty
- `⟶` Upload - prepare for transfer
- `⟷` Inherit - succession
- `⟸` Archive - long-term persistence

## Technical Foundation

Based on equilibrium-native computing principles derived from:
- Cybernetics (Norbert Wiener, 1948)
- Control Theory - Self-regulating systems
- Constraint Satisfaction Programming

## License

MIT License - Copyright (c) 2025-2026 Kevin Fain (ThēÆrchītēcť)

## Author

Kevin Fain - ThēÆrchītēcť
Contact: fabricatedkc@gmail.com

---

*S.I.S. - Sovereign Intelligence System*
*Equilibrium-native reasoning for personal AI*

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
