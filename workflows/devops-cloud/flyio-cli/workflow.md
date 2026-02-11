# flyio-cli

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/justinburdett/flyio-cli/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/justinburdett/flyio-cli/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Use the Fly.io flyctl CLI for deploying and operating apps on Fly.io. Default to read-only diagnostics (status/logs/config/releases). Only perform state-changing operations (deploys, SSH exec, secrets, scaling, machines, volumes, Postgres changes) with explicit user approval. Use when asked to deploy to Fly.io, debug fly deploy/build/runtime failures, set up GitHub Actions deploys/previews, or safely manage Fly apps and Postgres.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Use the Fly.io flyctl CLI for deploying and operating apps on Fly.io. Default to read-only diagnostics (status/logs/config/releases). Only perform state-changing operations (deploys, SSH exec, secrets, scaling, machines, volumes, Postgres changes) with explicit user approval. Use when asked to deploy to Fly.io, debug fly deploy/build/runtime failures, set up GitHub Actions deploys/previews, or safely manage Fly apps and Postgres.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run flyio-cli`)
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
You are executing the flyio-cli workflow. Use the following context:

Description: Use the Fly.io flyctl CLI for deploying and operating apps on Fly.io. Default to read-only diagnostics (status/logs/config/releases). Only perform state-changing operations (deploys, SSH exec, secrets, scaling, machines, volumes, Postgres changes) with explicit user approval. Use when asked to deploy to Fly.io, debug fly deploy/build/runtime failures, set up GitHub Actions deploys/previews, or safely manage Fly apps and Postgres.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: flyio-cli
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Fly.io (flyctl) CLI

Operate Fly.io apps safely and repeatably with `flyctl`.

## Defaults / safety

- Prefer **read-only** commands first: `fly status`, `fly logs`, `fly config show`, `fly releases`, `fly secrets list`.
- **Do not edit/modify Fly.io apps, machines, secrets, volumes, or databases without your human’s explicit approval.**
  - Read-only actions are OK without approval.
  - Destructive actions (destroy/drop) always require explicit approval.
- When debugging builds, capture the exact error output and determine whether it’s a:
  - build/packaging issue (Dockerfile, Gemfile.lock platforms, assets precompile)
  - runtime issue (secrets, DB, migrations)
  - platform issue (regions, machines, health checks)

## Quick start (typical deploy)

From the app repo directory:

1) Confirm which app you’re targeting
- `fly app list`
- `fly status -a <app>`
- Check `fly.toml` for `app = "..."`

2) Validate / inspect (read-only)
- `fly status -a <app>`
- `fly logs -a <app>`
- `fly config show -a <app>`

(Deploys are in **High-risk operations** below and require explicit user approval.)

## Debugging deploy/build failures

### Common checks
- `fly deploy --verbose` (more build logs)
- If using Dockerfile builds: verify Dockerfile Ruby/version and Gemfile.lock platforms match your builder OS/arch.

### Rails + Docker + native gems (nokogiri, pg, etc.)
Symptoms: Bundler can’t find a platform gem like `nokogiri-…-x86_64-linux` during build.

Fix pattern:
- Ensure `Gemfile.lock` includes the Linux platform used by Fly’s builder (usually `x86_64-linux`).
  - Example: `bundle lock --add-platform x86_64-linux`
- Ensure Dockerfile’s Ruby version matches `.ruby-version`.

(See `references/rails-docker-builds.md`.)

## Logs & config (read-only)

- Stream logs:
  - `fly logs -a <app>`
- Show config:
  - `fly config show -a <app>`
- List secrets (names only):
  - `fly secrets list -a <app>`

## High-risk operations (ask first)

These commands can execute arbitrary code on servers or mutate production state.
Only run them when the user explicitly asks you to.

- Deploy:
  - `fly deploy` / `fly deploy --remote-only`
- SSH exec / console:
  - `fly ssh console -a <app> -C "<command>"`
- Secrets changes:
  - `fly secrets set -a <app> KEY=value`

See `references/safety.md`.

## Fly Postgres basics

### Identify the Postgres app
- `fly postgres list`

### Attach Postgres to an app
- `fly postgres attach <pg-app> -a <app>`

### Create a database inside the cluster
- `fly postgres db create <db_name> -a <pg-app>`
- `fly postgres db list -a <pg-app>`

### Connect (psql)
- `fly postgres connect -a <pg-app>`

## GitHub Actions deploys / previews

- For production CD: use Fly’s GitHub Action (`superfly/flyctl-actions/setup-flyctl`) and run `flyctl deploy`.
- For PR previews:
  - Prefer one **preview app per PR** and one **database per PR** inside a shared Fly Postgres cluster.
  - Automate create/deploy/comment on PR; destroy on close.

(See `references/github-actions.md`.)

## Bundled resources

- `references/safety.md`: safety rules (read-only by default; ask before mutating state).
- `references/rails-docker-builds.md`: Rails/Docker/Fly build failure patterns + fixes.
- `references/github-actions.md`: Fly deploy + preview workflows.
- `scripts/fly_app_from_toml.sh`: tiny helper to print the Fly app name from fly.toml (shell-only; no ruby).

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
