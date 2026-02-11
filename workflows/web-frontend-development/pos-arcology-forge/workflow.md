# pos-arcology-forge

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kunoiiv/pos-arcology-forge/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kunoiiv/pos-arcology-forge/SKILL.md)
> Category: Web & Frontend Development

---

## Description

PoW-verified Elysium Arcology Planner + Hub. Grind nonces on O'Neill sims/exosuits (physics/3D exports) → trustless shares for P2P hub. Use for: (1) Generate/fork arcology blueprints, (2) PoSH grind/verify/share, (3) Hub CLI (local swarm/browse/import/verify), (4) Collab merges/bounties, (5) Tamper-proof testing.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
PoW-verified Elysium Arcology Planner + Hub. Grind nonces on O'Neill sims/exosuits (physics/3D exports) → trustless shares for P2P hub. Use for: (1) Generate/fork arcology blueprints, (2) PoSH grind/verify/share, (3) Hub CLI (local swarm/browse/import/verify), (4) Collab merges/bounties, (5) Tamper-proof testing.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run pos-arcology-forge`)
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
You are executing the pos-arcology-forge workflow. Use the following context:

Description: PoW-verified Elysium Arcology Planner + Hub. Grind nonces on O'Neill sims/exosuits (physics/3D exports) → trustless shares for P2P hub. Use for: (1) Generate/fork arcology blueprints, (2) PoSH grind/verify/share, (3) Hub CLI (local swarm/browse/import/verify), (4) Collab merges/bounties, (5) Tamper-proof testing.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: pos-arcology-forge
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# PoSH Arcology Forge (V1.2 - Ultimate Bulletproof)

BTC PoW for antifragile orbital blueprints. Full edge-coverage: tamper-evident, timeouts, clamps, tests.

## Quick Start
```bash
node scripts/pos-share.js '{\"radius_km\":3,\"pop_m\":500000}'  # E2E → share.pos.json
node scripts/pos-grind.js share.pos.json --verify              # ✅ VALID
node scripts/hub-cli.js import share.pos.json
node scripts/hub-cli.js list                                   # Valid only
node scripts/test.js                                           # Full suite
```

## Workflow (Ironclad)
1. **Params** → Schema/validate/clamp.
2. **Sim** → Physics (no crash).
3. **Grind** → Timeout/progress/tamper-proof.
4. **Hub** → Verify on ops.

**Exports**: grind/verify/treeHash (importable).

See refs for physics/exosuits.

## Scripts
- All async/try-catch, stdlib only.
- `test.js`: Auto-runs edges (good/bad/tamper).

Prod: 100% bulletproof (20+ cases).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
