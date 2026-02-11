# elysium-arcology-planner

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kunoiiv/elysium-arcology-planner/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kunoiiv/elysium-arcology-planner/SKILL.md)
> Category: AI & LLMs

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
**Trigger:** User-invocable (via `aidarr run elysium-arcology-planner`)
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
You are executing the elysium-arcology-planner workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: elysium-arcology-planner
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Elysium Arcology Planner

Scale humanity: Design self-sustaining orbital arcologies. Infuse BTC sovereignty—sats-secured blueprints, immersion-cooled mining rigs in habitats.

## Quick Start Workflow
1. **Snapshot canvas**: `canvas action=snapshot` → base UI state.
2. **Present interactive canvas**: `canvas action=present url=arcology.html x=100 y=100 width=1200 height=800` (drag components).
3. **Eval designs**: `canvas action=eval javaScript=simulateGravity(...)` for physics/power sims.
4. **AR overlay**: `nodes action=camera_snap node=desk-cam` → project design via canvas/navigate.
5. **Export blueprint**: `python scripts/export-svg-to-3d.py assets/leg.svg` → FreeCAD/STL.

## Components (Drag from Palette)
- **O'Neill Cylinder**: 8km dia, 32km long, 10k pop. Blueprint: NASA public domain (Toroidal agri-rings). Calc: Spin=1RPM → 1G.
- **Fusion Reactor**: Tokamak/Stellarator. Open-source: Wendelstein 7-X coils (Greifswald data). Output: 1GW, immersion-cooled.
- **Neuralink Hub**: Collective IQ node. Sim: Bandwidth to 1M minds.
- **Exosuit Factory**: OpenExo arms/legs (GitHub: servo+PWM+H-bridges). Print: Replicators → 100/day. Naubiomech leg spec: [naubiomech-leg-spec.md](./references/naubiomech-leg-spec.md).
- **ASIC Mining Bay**: Solar-powered hashrate farms. Tie to BTC node.

## Scripts (Run via exec)
- `scripts/sim-physics.py`: Gravity/power/Coriolis calcs (JSON stdin → metrics). Ex: `echo '{"rpm":1}' | python scripts/sim-physics.py`.
- `scripts/export-svg-to-3d.py`: SVG → FreeCAD JSON/STL (parses leg.svg → extrusions/cyls).

## References (Read as Needed)
- [oneill-blueprints.md](./references/oneill-blueprints.md): NASA Princeton '76 studies.
- [exosuit-openexo.md](./references/exosuit-openexo.md): GitHub BOMs, CAD.
- [fusion-stellarator.md](./references/fusion-stellarator.md): Open plasma designs.
- [naubiomech-leg-spec.md](./references/naubiomech-leg-spec.md): Modular leg BOM/physics.

## Assets
- `assets/components.svg`: Drag icons (cylinder, reactor...).
- `assets/arcology-template.html`: Canvas boilerplate w/ Fabric.js.
- `assets/leg.svg`: Naubiomech leg blueprint.

## Pro Tips
- **Scale sim**: Eval total mass/power/pop/hashrate. Alert if > asteroid belt viable.
- **BTC integration**: Add mining rig—hashrate vs. energy budget.
- **Node AR**: Snap desk cam → overlay design for "print this exosuit".
- **PowerShell Fix**: Use `;` not `&&` for chaining (e.g., `cd dir; python script.py`).
- Iterate: Edit canvas → snapshot → share sats-secured fork (proof-of-share).

Test: `canvas action=present` a basic cylinder + reactor. Boom—Elysium draft.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
