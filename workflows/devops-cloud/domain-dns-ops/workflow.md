# domain-dns-ops

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/steipete/domain-dns-ops/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/steipete/domain-dns-ops/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Domain/DNS ops across Cloudflare, DNSimple, Namecheap for Peter. Use for onboarding zones to Cloudflare, flipping nameservers, setting redirects (Page Rules/Rulesets/Workers), updating redirect-worker mappings, and verifying DNS/HTTP. Source of truth: ~/Projects/manager.


**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Domain/DNS ops across Cloudflare, DNSimple, Namecheap for Peter. Use for onboarding zones to Cloudflare, flipping nameservers, setting redirects (Page Rules/Rulesets/Workers), updating redirect-worker mappings, and verifying DNS/HTTP. Source of truth: ~/Projects/manager.


### O - Orchestration
**Trigger:** User-invocable (via `aidarr run domain-dns-ops`)
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
You are executing the domain-dns-ops workflow. Use the following context:

Description: Domain/DNS ops across Cloudflare, DNSimple, Namecheap for Peter. Use for onboarding zones to Cloudflare, flipping nameservers, setting redirects (Page Rules/Rulesets/Workers), updating redirect-worker mappings, and verifying DNS/HTTP. Source of truth: ~/Projects/manager.


Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: domain-dns-ops
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Domain/DNS Ops (Peter)

This skill is a thin router: use `~/Projects/manager` as truth, run the repo scripts, follow the checklists.

## Source of truth (read first)

- `~/Projects/manager/DOMAINS.md` (domain -> target map; registrar hints; exclusions)
- `~/Projects/manager/DNS.md` (Cloudflare onboarding + DNS/redirect checklist)
- `~/Projects/manager/redirect-worker.ts` + `~/Projects/manager/redirect-worker-mapping.md` (worker redirects)

## Golden path (new vanity domain -> Cloudflare -> redirect)

1. **Decide routing model**
   - Page Rule redirect (small scale, per-zone).
   - Rulesets / Bulk Redirects (account-level; needs token perms).
   - Worker route (fallback; uses `redirect-worker`).
2. **Cloudflare zone**
   - Create zone (UI), then confirm with `cli4`:
     - `cli4 --get name=example.com /zones`
3. **Nameservers**
   - If registrar = Namecheap: `cd ~/Projects/manager && source profile && bin/namecheap-set-ns example.com emma.ns.cloudflare.com scott.ns.cloudflare.com`
   - If registrar = DNSimple: see `~/Projects/manager/DNS.md` for delegation API notes.
4. **DNS placeholders (so CF can terminate HTTPS)**
   - Proxied apex `A` + wildcard `A` → `192.0.2.1` (see `~/Projects/manager/DNS.md` for exact `cli4` calls).
5. **Redirect**
   - If using Page Rules: use the `cli4 --post ... /pagerules` template from `~/Projects/manager/DNS.md`.
   - If using Worker: update mapping (`~/Projects/manager/redirect-worker-mapping.md`), deploy/bind routes per `~/Projects/manager/DNS.md`.
6. **Verify**
   - DNS: `dig +short example.com @1.1.1.1` (expect CF anycast).
   - HTTPS redirect: `curl -I https://example.com` (expect `301`).

## Common ops

- **Cloudflare token sanity**: `source ~/.profile` (prefer `CLOUDFLARE_API_TOKEN`; `CF_API_TOKEN` fallback).
- **Disable “Block AI bots”**: `cd ~/Projects/manager && source profile && bin/cloudflare-ai-bots status` / `bin/cloudflare-ai-bots disable`.

## After edits (commit/push)

If you changed anything in `~/Projects/manager` (docs, worker, scripts, mappings): commit there too.

1. Review: `cd ~/Projects/manager && git status && git diff`
2. Stage: `git add <paths>`
3. Commit (Conventional Commits): `git commit -m "feat: …"` / `fix:` / `docs:` / `chore:`
4. Push only when explicitly asked: `git push origin main`

## Guardrails

- Don’t touch `.md` lore domains or `steipete.md` unless explicitly asked; check `~/Projects/manager/DOMAINS.md`.
- Confirm registrar before debugging CF “invalid nameservers” (often “wrong registrar”).
- Prefer reversible steps; verify after each change (NS → DNS → redirect).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
