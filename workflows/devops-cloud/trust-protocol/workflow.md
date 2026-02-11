# trust-protocol

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/felmonon/trust-protocol/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/felmonon/trust-protocol/SKILL.md)
> Category: DevOps & Cloud

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
**Trigger:** User-invocable (via `aidarr run trust-protocol`)
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
You are executing the trust-protocol workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: trust-protocol
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Agent Trust Protocol (ATP)

Establish, verify, and maintain trust between AI agents. Bayesian trust scoring with domain-specific trust, revocation, forgetting curves, and a visual dashboard.

## Install

```bash
git clone https://github.com/FELMONON/trust-protocol.git
# No dependencies beyond Python 3.8+ stdlib
# Pair with skillsign for identity: https://github.com/FELMONON/skillsign
```

## Quick Start

```bash
# Add an agent to your trust graph
python3 atp.py trust add alpha --fingerprint "abc123" --score 0.7

# Record interactions — trust evolves via Bayesian updates
python3 atp.py interact alpha positive --note "Delivered clean code"
python3 atp.py interact alpha positive --domain code --note "Tests passing"

# Check trust
python3 atp.py trust score alpha
python3 atp.py trust domains alpha

# View the full graph
python3 atp.py status
python3 atp.py graph export --format json

# Run the full-stack demo (identity → trust → dashboard)
python3 demo.py --serve
```

## Commands

### Trust Management
```bash
atp.py trust add <agent> --fingerprint <fp> [--domain <d>] [--score <0-1>]
atp.py trust list
atp.py trust score <agent>
atp.py trust remove <agent>
atp.py trust revoke <agent> [--reason <reason>]
atp.py trust restore <agent> [--score <0-1>]
atp.py trust domains <agent>
```

### Interactions
```bash
atp.py interact <agent> <positive|negative> [--domain <d>] [--note <note>]
```

### Challenge-Response
```bash
atp.py challenge create <agent>
atp.py challenge respond <challenge_file>
atp.py challenge verify <response_file>
```

### Graph
```bash
atp.py graph show
atp.py graph path <from> <to>
atp.py graph export [--format json|dot]
atp.py status
```

### Dashboard
```bash
python3 serve_dashboard.py          # localhost:8420
python3 demo.py --serve             # full demo + dashboard
```

### Moltbook Integration
```bash
python3 moltbook_trust.py verify <agent>    # check agent trust via Moltbook profile
```

## How Trust Works

- **Bayesian updates**: Each interaction shifts trust scores with diminishing deltas (prevents thrashing)
- **Negativity bias**: Negative interactions hit harder than positive ones boost
- **Domain-specific**: Trust an agent for code but not for security advice
- **Forgetting curves**: Trust decays without interaction (R = e^(-t/S))
- **Revocation**: Immediate drop to floor, restorable at reduced score
- **Transitive trust**: If you trust A and A trusts B, you partially trust B (with decay)

## Integration with skillsign

ATP builds on [skillsign](https://github.com/FELMONON/skillsign) for identity:
1. Agents generate ed25519 keypairs with skillsign
2. Agents sign skills, others verify signatures
3. Verified agents get added to the ATP trust graph
4. Interactions update trust scores over time

## Triggers
"check trust", "trust score", "trust graph", "verify agent", "agent trust", "trust status", "who do I trust", "trust report"

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
