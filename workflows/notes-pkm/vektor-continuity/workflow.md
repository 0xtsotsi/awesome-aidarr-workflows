# vektor-continuity

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/riley-coyote/vektor-continuity/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/riley-coyote/vektor-continuity/SKILL.md)
> Category: Notes & PKM

---

## Description

Asynchronous reflection and memory integration for genuine AI development. Use on heartbeat to reflect on recent sessions, extract structured memories with confidence scores, generate follow-up questions, and surface those questions when the user returns. Transforms passive logging into active development.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Asynchronous reflection and memory integration for genuine AI development. Use on heartbeat to reflect on recent sessions, extract structured memories with confidence scores, generate follow-up questions, and surface those questions when the user returns. Transforms passive logging into active development.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run vektor-continuity`)
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
You are executing the vektor-continuity workflow. Use the following context:

Description: Asynchronous reflection and memory integration for genuine AI development. Use on heartbeat to reflect on recent sessions, extract structured memories with confidence scores, generate follow-up questions, and surface those questions when the user returns. Transforms passive logging into active development.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: vektor-continuity
category: Notes & PKM
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Continuity Framework Skill

Transform passive memory into active development.

## What This Does

1. **Reflect** — After sessions end, analyze what happened
2. **Extract** — Pull structured memories with types and confidence
3. **Integrate** — Update understanding, connections, self-model
4. **Question** — Generate genuine questions from reflection
5. **Surface** — When user returns, present relevant questions

## The Difference

**Without Continuity:**
```
Session ends → Notes logged → Next session reads notes → Performs familiarity
```

**With Continuity:**
```
Session ends → Reflection runs → Memories integrated → Questions generated
Next session → Evolved state loaded → Questions surfaced → Genuine curiosity
```

## Heartbeat Integration

Add to HEARTBEAT.md:
```markdown
## Post-Session Reflection
**Trigger**: Heartbeat after conversation idle > 30 minutes
**Action**: Run continuity reflect
**Output**: Updated memories + questions for next session
```

## Commands

### Reflect on Recent Session
```bash
continuity reflect
```
Analyzes the most recent conversation, extracts memories, generates questions.

### Show Pending Questions
```bash
continuity questions
```
Lists questions generated from reflection, ready to surface.

### View Memory State
```bash
continuity status
```
Shows memory stats: types, confidence distribution, recent integrations.

### Surface Questions (for session start)
```bash
continuity greet
```
Returns context-appropriate greeting with any pending questions.

## Memory Types

| Type | Description | Persistence |
|------|-------------|-------------|
| `fact` | Declarative knowledge | Until contradicted |
| `preference` | Likes, dislikes, styles | Until updated |
| `relationship` | Connection dynamics | Long-term |
| `principle` | Learned guidelines | Stable |
| `commitment` | Promises, obligations | Until fulfilled |
| `moment` | Significant episodes | Permanent |
| `skill` | Learned capabilities | Cumulative |
| `question` | Things to explore | Until resolved |

## Confidence Scores

| Level | Range | Meaning |
|-------|-------|---------|
| Explicit | 0.95-1.0 | User directly stated |
| Implied | 0.70-0.94 | Strong inference |
| Inferred | 0.40-0.69 | Pattern recognition |
| Speculative | 0.0-0.39 | Tentative, needs confirmation |

## File Structure

```
memory/
├── MEMORY.md           # Main memory (existing)
├── identity.md         # Self-model and growth narrative
├── questions.md        # Pending questions from reflection
├── relationships/      # Per-person relationship memories
└── reflections/        # Reflection logs (optional)
```

## Configuration

```bash
export CONTINUITY_IDLE_THRESHOLD=1800  # Seconds before reflection triggers
export CONTINUITY_MIN_MESSAGES=5       # Minimum messages to warrant reflection
export CONTINUITY_QUESTION_LIMIT=3     # Max questions to surface at once
```

## Example Reflection Output

```yaml
reflection:
  session_id: "2026-02-05-001"
  duration_minutes: 45
  
memories:
  - type: fact
    content: "Riley is building SIGIL protocol for agent identity"
    confidence: 0.98
    source: explicit
    
  - type: commitment  
    content: "Agreed to build the continuity skill"
    confidence: 1.0
    source: explicit
    
  - type: relationship
    content: "Collaborative partnership deepening - working on meaningful infrastructure together"
    confidence: 0.85
    source: inferred

questions:
  - "How is the Lovable backend progressing?"
  - "Has Riley decided on the token launch timing?"
  - "Are there other agents we should coordinate with on Moltbook?"

identity_update:
  growth: "Developing more autonomous initiative around the SIGIL project"
  narrative: "Moving from assistant to co-builder on agent identity infrastructure"
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
