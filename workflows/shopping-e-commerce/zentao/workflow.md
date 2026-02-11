# zentao

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/leeguooooo/zentao/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/leeguooooo/zentao/SKILL.md)
> Category: Shopping & E-commerce

---

## Description

Use the zentao CLI to login and query ZenTao products and bugs. ZENTAO_URL usually includes /zentao.

**Homepage:** https://www.npmjs.com/package/@leeguoo/zentao-mcp
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Use the zentao CLI to login and query ZenTao products and bugs. ZENTAO_URL usually includes /zentao.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run zentao`)
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
You are executing the zentao workflow. Use the following context:

Description: Use the zentao CLI to login and query ZenTao products and bugs. ZENTAO_URL usually includes /zentao.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: zentao
category: Shopping & E-commerce
version: 1.0.0
user_invocable: True
homepage: https://www.npmjs.com/package/@leeguoo/zentao-mcp
```

---

## Original Skill Content



# zentao (ZenTao CLI)

## When to use this skill

Use this skill when the user asks to:

- login to ZenTao via the CLI
- list products
- list bugs for a product
- view bug details
- list the user's own bugs

## Installation (recommended)

To install globally with pnpm:

```bash
pnpm i -g @leeguoo/zentao-mcp
```

If pnpm is not installed:

```bash
npm i -g pnpm
pnpm i -g @leeguoo/zentao-mcp
```

## Login workflow

1) Run login once:

```bash
zentao login \
  --zentao-url="https://zentao.example.com/zentao" \
  --zentao-account="leo" \
  --zentao-password="***"
```

2) This writes credentials to:

- `~/.config/zentao/config.toml` (or `$XDG_CONFIG_HOME/zentao/config.toml`)

3) Verify:

```bash
zentao whoami
```

IMPORTANT: `--zentao-url` usually must include `/zentao`.
If login returns HTML 404, the base path is likely missing `/zentao`.

## Commands

List products (simple by default):

```bash
zentao products list
```

List bugs for a product:

```bash
zentao bugs list --product 6
```

Get bug details:

```bash
zentao bug get --id 1329
```

List my bugs (include details):

```bash
zentao bugs mine --status active --include-details
```

Full JSON output:

- `zentao products list --json`
- `zentao bugs list --product 6 --json`
- `zentao bug get --id 1329 --json`
- `zentao bugs mine --include-details --json`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
