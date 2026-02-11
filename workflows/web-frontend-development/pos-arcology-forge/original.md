



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
