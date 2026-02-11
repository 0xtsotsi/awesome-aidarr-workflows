# claude-optimised

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/hexnickk/claude-optimised/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/hexnickk/claude-optimised/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Guide for writing and optimizing CLAUDE.md files for maximum Claude Code performance. Use when creating new CLAUDE.md, reviewing existing ones, or when user asks about CLAUDE.md best practices. Covers structure, content, pruning, and common mistakes.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Guide for writing and optimizing CLAUDE.md files for maximum Claude Code performance. Use when creating new CLAUDE.md, reviewing existing ones, or when user asks about CLAUDE.md best practices. Covers structure, content, pruning, and common mistakes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run claude-optimised`)
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
You are executing the claude-optimised workflow. Use the following context:

Description: Guide for writing and optimizing CLAUDE.md files for maximum Claude Code performance. Use when creating new CLAUDE.md, reviewing existing ones, or when user asks about CLAUDE.md best practices. Covers structure, content, pruning, and common mistakes.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: claude-optimised
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# CLAUDE.md Optimization Guide

Write CLAUDE.md files that maximize Claude's adherence and performance.

## Core Principle: Less Is More

Long CLAUDE.md = Claude ignores half of it. Critical rules get lost in noise.

**For each line ask:** "Would removing this cause Claude to make mistakes?"
- If no → delete it
- If Claude already does it correctly → delete it or convert to hook

## What to Include

### Essential (High Value)

| Section | Example |
|---------|---------|
| Project context | "Next.js e-commerce app with Stripe" (1 line) |
| Build/test commands | `npm run test`, `pnpm build` |
| Critical gotchas | "Never modify auth.ts directly" |
| Non-obvious conventions | "Use `vi` for state, not `useState`" |
| Domain terminology | "PO = Purchase Order, not Product Owner" |

### Include Only If Non-Standard

- Branch naming (if not `feature/`, `fix/`)
- Commit format (if not conventional commits)
- File boundaries (sensitive files to avoid)

### Do NOT Include

- Things Claude already knows (general coding practices)
- Obvious patterns (detectable from existing code)
- Lengthy explanations (be terse)
- Aspirational rules (only real problems you've hit)

## Structure

```markdown
# Project Name

One-line description.

## Commands
- Test: `npm test`
- Build: `npm run build`
- Lint: `npm run lint`

## Code Style
- [Only non-obvious conventions]

## Architecture
- [Brief, only if complex]

## IMPORTANT
- [Critical warnings - use sparingly]
```

## Formatting Rules

- **Bullet points** over paragraphs
- **Markdown headings** to separate modules (prevents instruction bleed)
- **Specific** over vague: "2-space indent" not "format properly"
- **IMPORTANT/YOU MUST** for critical rules (use sparingly or loses effect)

## File Placement

| Location | Scope |
|----------|-------|
| `~/.claude/CLAUDE.md` | All sessions (user prefs) |
| `./CLAUDE.md` | Project root (share via git) |
| `./subdir/CLAUDE.md` | Loaded when working in subdir |
| `.claude/rules/*.md` | Auto-loaded as project memory |

## Optimization Checklist

Before finalizing:
- [ ] Under 50 lines? (ideal target)
- [ ] Every line solves a real problem you've encountered?
- [ ] No redundancy with other CLAUDE.md locations?
- [ ] No instructions Claude follows by default?
- [ ] Tested by observing if Claude's behavior changes?

## Maintenance

- Run `/init` as starting point, then prune aggressively
- Every few weeks: "Review this CLAUDE.md and suggest removals"
- When Claude misbehaves: add specific rule
- When Claude ignores rules: file too long, prune other content

## Anti-Patterns

| Don't | Why |
|-------|-----|
| 200+ line CLAUDE.md | Gets ignored |
| "Write clean code" | Claude knows this |
| Duplicate rules across files | Wastes tokens, conflicts |
| Theoretical concerns | Only add for real problems |
| Long prose explanations | Use bullet points |

## Example: Minimal Effective CLAUDE.md

```markdown
# MyApp

React Native app with Expo. Backend is Supabase.

## Commands
- `pnpm test` - run tests
- `pnpm ios` - run iOS simulator

## Style
- Prefer Zustand over Context
- Use `clsx` for conditional classes

## IMPORTANT
- NEVER commit .env files
- Auth logic lives in src/lib/auth.ts only
```

~15 lines. Covers what Claude can't infer. Nothing more.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
