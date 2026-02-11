# release-bump

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/paulpete/release-bump/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/paulpete/release-bump/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Use when bumping ralph-orchestrator version for a new release, after fixes are committed and ready to publish

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Use when bumping ralph-orchestrator version for a new release, after fixes are committed and ready to publish

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run release-bump`)
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
You are executing the release-bump workflow. Use the following context:

Description: Use when bumping ralph-orchestrator version for a new release, after fixes are committed and ready to publish

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: release-bump
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Release Bump

## Overview

Bump version and trigger release for ralph-orchestrator. All versions live in workspace `Cargo.toml` - individual crates inherit via `version.workspace = true`.

Confirm the new version with the user. Once the bump commit is pushed, track progress of the release.

## Quick Reference

| Step | Command/Action |
|------|----------------|
| 1. Bump version | Edit `Cargo.toml`: replace all `version = "X.Y.Z"` (7 occurrences) |
| 2. Build | `cargo build` (updates Cargo.lock) |
| 3. Test | `cargo test` |
| 4. Commit | `git add Cargo.toml Cargo.lock && git commit -m "chore: bump to vX.Y.Z"` |
| 5. Push | `git push origin main` |
| 6. Tag | `git tag vX.Y.Z && git push origin vX.Y.Z` |

## Version Locations (All in Cargo.toml)

```toml
# Line ~17 - workspace version
[workspace.package]
version = "X.Y.Z"

# Lines ~113-118 - internal crate dependencies
ralph-proto = { version = "X.Y.Z", path = "crates/ralph-proto" }
ralph-core = { version = "X.Y.Z", path = "crates/ralph-core" }
ralph-adapters = { version = "X.Y.Z", path = "crates/ralph-adapters" }
ralph-tui = { version = "X.Y.Z", path = "crates/ralph-tui" }
ralph-cli = { version = "X.Y.Z", path = "crates/ralph-cli" }
ralph-bench = { version = "X.Y.Z", path = "crates/ralph-bench" }
```

**Tip:** Use Edit tool with `replace_all: true` on `version = "OLD"` → `version = "NEW"` to update all 7 at once.

## What CI Does Automatically

Once you push the tag, `.github/workflows/release.yml` triggers and:

1. Creates the GitHub Release with auto-generated notes
2. Builds binaries for macOS (arm64, x64) and Linux (arm64, x64)
3. Uploads artifacts to the GitHub Release
4. Publishes to crates.io (in dependency order)
5. Publishes to npm as `@ralph-orchestrator/ralph`

## Common Mistakes

| Mistake | Fix |
|---------|-----|
| Only updating workspace.package.version | Must update all 7 occurrences including internal deps |
| Forgetting to run tests | Always `cargo test` before commit |
| Creating release manually with `gh release create` | Just push the tag - CI creates the release with artifacts |
| Pushing tag before main | Push main first, then push the tag |


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
