# satori

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/joelachance/satori/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/joelachance/satori/SKILL.md)
> Category: Notes & PKM

---

## Description

Persistent long term memory for for continuity in ai sessions between providers and codegen tools.

TRIGGERS - Activate this skill when:
- User explicitly mentions "satori", "remember this", "save", "add",  "save this for later", "store this", "add to memory"
- User asks to recall/search past decisions: "what did we decide", "remind me", "search my notes", "what do I know about"
- Conversation contains notable facts worth persisting: decisions, preferences, deadlines, names, tech stack choices, strategic directions
- Starting a new conversation where proactive context retrieval would help
- Use Satori search when user asks a question


**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Persistent long term memory for for continuity in ai sessions between providers and codegen tools.

TRIGGERS - Activate this skill when:
- User explicitly mentions "satori", "remember this", "save", "add",  "save this for later", "store this", "add to memory"
- User asks to recall/search past decisions: "what did we decide", "remind me", "search my notes", "what do I know about"
- Conversation contains notable facts worth persisting: decisions, preferences, deadlines, names, tech stack choices, strategic directions
- Starting a new conversation where proactive context retrieval would help
- Use Satori search when user asks a question


### O - Orchestration
**Trigger:** User-invocable (via `aidarr run satori`)
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
You are executing the satori workflow. Use the following context:

Description: Persistent long term memory for for continuity in ai sessions between providers and codegen tools.

TRIGGERS - Activate this skill when:
- User explicitly mentions "satori", "remember this", "save", "add",  "save this for later", "store this", "add to memory"
- User asks to recall/search past decisions: "what did we decide", "remind me", "search my notes", "what do I know about"
- Conversation contains notable facts worth persisting: decisions, preferences, deadlines, names, tech stack choices, strategic directions
- Starting a new conversation where proactive context retrieval would help
- Use Satori search when user asks a question


Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: satori
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Satori CLI Integration

Satori persists notable information across AI applications. It stores facts in both vector and knowledge graph databases for later retrieval.

## Environment Requirements

**Works in:** Claude Code, Cursor, Windsurf, or any AI tool with local terminal access.

## Authentication

The CLI auto-configures on first run:
- Checks `~/.config/satori/satori.json` for API key and memory ID
- If missing, creates the file and provisions new credentials automatically
- No manual setup required

## CLI Commands

**Save facts:**
```bash
npx -y @satori-sh/cli@latest add "<facts>"
```

**Search for context:**
```bash
npx -y @satori-sh/cli@latest search "<query>"
```

## Workflow: Proactive Search

At conversation start, if the user's message suggests existing context would help:

1. Extract key entities/topics from user's first message
2. Run search command with relevant query
3. Parse JSON response to extract relevant facts
4. Silently incorporate retrieved context into response
5. Do NOT announce "I searched Satori" unless results significantly impact the response

**Parsing search results:**
The CLI returns JSON. Extract the relevant facts and use them as context:
```bash
npx -y @satori-sh/cli search "Flamingo project tech stack"
# Returns JSON with matching facts - parse and incorporate naturally
```

Example triggers for proactive search:
- "Let's continue working on [project]"
- "What's the status of [thing]"
- References to past decisions without full context
- Project names, company names, people names

## Workflow: Save Facts

### When to Save

Save at natural breakpoints:
- End of a decision-making discussion
- When user explicitly requests ("remember this", "save this")
- After establishing concrete preferences, names, dates, deadlines
- When significant project context is established

### What to Save

See `references/fact-criteria.md` for detailed criteria.

**SAVE** - Notable, persistent information:
- Decisions: "Using PostgreSQL for the database"
- Tech preferences: "User prefers Bun over Node"
- Names/branding: "Company name is Flamingo, they make pink cookies"
- Dates/deadlines: "MVP deadline is March 15"
- Architecture choices: "Microservices with event sourcing"
- Strategic directions: "Targeting enterprise customers first"
- Key contacts: "Sarah is the design lead"
- Project context: "Satori is an AI memory infrastructure company"

**DO NOT SAVE** - Transient, granular, or obvious:
- Work-in-progress feedback: "the color scheme needs work"
- Claude's explanations or code snippets
- Temporary debugging context
- Generic preferences derivable from context
- Conversational filler

### Save Execution

1. Extract notable facts from conversation (see criteria)
2. Format as natural language, batch related facts together
3. Execute CLI command
4. On success: continue silently (fire-and-forget)
5. On failure: notify user with error

**Batching:** The API handles batching, so longer natural language text is fine:
```bash
npx -y @satori-sh/cli add "User is building Satori, an AI memory infrastructure company. Tech stack: TypeScript, Bun, PostgreSQL. Deadline for MVP is March 15. Targeting developer tools market initially."
```

## Error Handling

If CLI fails or isn't installed:
```
⚠️ Satori CLI error: [error message]
To install: npm install -g @satori-sh/cli
Facts were not saved. Would you like me to show what I attempted to save?
```

## Fact Formatting

Write facts as clear, standalone statements. Include context so facts make sense when retrieved later:

**Good:** "Satori project uses PostgreSQL for primary storage and FalkorDB for knowledge graphs"
**Bad:** "Using Postgres and FalkorDB"

**Good:** "User prefers Bun runtime over Node.js for all JavaScript/TypeScript projects"
**Bad:** "Bun not Node"
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
