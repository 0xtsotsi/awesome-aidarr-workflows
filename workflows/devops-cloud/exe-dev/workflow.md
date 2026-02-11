# exe-dev

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/bjesuiter/exe-dev/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/bjesuiter/exe-dev/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Manage persistent VMs on exe.dev. Create VMs, configure HTTP proxies, share access, and set up custom domains. Use when working with exe.dev VMs for hosting, development, or running persistent services.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage persistent VMs on exe.dev. Create VMs, configure HTTP proxies, share access, and set up custom domains. Use when working with exe.dev VMs for hosting, development, or running persistent services.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run exe-dev`)
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
You are executing the exe-dev workflow. Use the following context:

Description: Manage persistent VMs on exe.dev. Create VMs, configure HTTP proxies, share access, and set up custom domains. Use when working with exe.dev VMs for hosting, development, or running persistent services.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: exe-dev
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



> ⚠️ **Warning:** This skill was auto-built by clawdbot from the exe.dev markdown documentation. It's not tested yet — use with caution! I plan to test it soon. 🔜

# exe.dev VM Management

## Quick Commands

| Task | Command |
|------|---------|
| List VMs | `ssh exe.dev ls --json` |
| Create VM | `ssh exe.dev new` |
| Make public | `ssh exe.dev share set-public <vm>` |
| Change port | `ssh exe.dev share port <vm> <port>` |
| Add user | `ssh exe.dev share add <vm> <email>` |
| Share link | `ssh exe.dev share add-link <vm>` |

## Access URLs

- **VM**: `https://<vmname>.exe.xyz/`
- **Shelley agent**: `https://<vmname>.exe.xyz:9999/`
- **VSCode**: `vscode://vscode-remote/ssh-remote+<vmname>.exe.xyz/home/exedev`

## Proxy Configuration

Default port is auto-selected from Dockerfile EXPOSE. Change with:
```bash
ssh exe.dev share port <vmname> <port>
```

Access ports 3000-9999 via `https://vmname.exe.xyz:<port>/`

## Authentication Headers

When users authenticate via exe.dev:
- `X-ExeDev-UserID` — user identifier
- `X-ExeDev-Email` — user email

For testing, use mitmproxy to inject headers:
```bash
mitmdump --mode reverse:http://localhost:8000 --listen-port 3000 \
  --set modify_headers='/~q/X-ExeDev-Email/user@example.com'
```

## Custom Domains

- **Subdomains**: CNAME `app.example.com` → `vmname.exe.xyz`
- **Apex**: ALIAS `example.com` → `exe.xyz` + CNAME `www` → `vmname.exe.xyz`

## Full Reference

See [references/exe-dev-vm-service.md](exe-dev-vm-service.md) for complete documentation including pricing, Shelley agent setup, SSH key config, and FAQ.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
