# hivefence

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/seojoonkim/hivefence/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/seojoonkim/hivefence/SKILL.md)
> Category: AI & LLMs

---

## Description

Collective immunity network for AI agents. When one agent detects a prompt injection attack, all connected agents become immune. Real-time pattern detection, community voting, and distributed threat intelligence. Built on top of prompt-guard.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Collective immunity network for AI agents. When one agent detects a prompt injection attack, all connected agents become immune. Real-time pattern detection, community voting, and distributed threat intelligence. Built on top of prompt-guard.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run hivefence`)
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
You are executing the hivefence workflow. Use the following context:

Description: Collective immunity network for AI agents. When one agent detects a prompt injection attack, all connected agents become immune. Real-time pattern detection, community voting, and distributed threat intelligence. Built on top of prompt-guard.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: hivefence
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# HiveFence v1.0.0

🐝 **When one is attacked, all become immune.**

Collective prompt injection defense network for AI agents.

## What is HiveFence?

HiveFence extends prompt-guard with a distributed immunity system:

1. **Detect** — Your agent scans incoming prompts against 15+ attack patterns
2. **Report** — New attack patterns are hashed and submitted to the network
3. **Immunize** — Community validates the pattern, then every connected agent gets the update

## Features

- 🔍 **Real-time Detection** — Pattern matching + semantic analysis in <50ms
- 🌍 **Multi-language** — EN, KO, JA, ZH attack detection
- 🗳️ **Community Governance** — Democratic voting on new patterns
- 🔐 **Privacy-preserving** — Only SHA-256 hashes shared, not raw content
- 📊 **Severity Scoring** — Risk-based prioritization (0-100)
- ⚡ **Edge-first** — Cloudflare Workers at 300+ locations

## Installation

```bash
# Via ClawdHub
npx clawhub install hivefence

# Or via npm
npm install hivefence
```

## Quick Start

```javascript
import { protect, reportThreat } from 'hivefence'

// Scan incoming prompt
const result = await protect(userInput)

if (result.blocked) {
  console.log(`Threat blocked: ${result.category}`)
  // Pattern automatically reported to network
}
```

## Security Stack Recommendation

For maximum protection, use HiveFence with:

1. **ACIP** — Advanced Cognitive Inoculation Prompt (behavioral boundaries)
2. **HiveFence** — Pattern detection + collective immunity
3. **SkillGuard** — Audit skills before installation

As recommended in [@VittoStack's Security Guide](https://x.com/vittostack/status/2018326025373900881) (34K+ views)

## API Endpoints

| Method | Endpoint | Description |
|--------|----------|-------------|
| POST | `/api/v1/threats/report` | Submit new threat pattern |
| GET | `/api/v1/threats/pending` | Get patterns awaiting votes |
| POST | `/api/v1/threats/:id/vote` | Vote on a pattern |
| GET | `/api/v1/threats/latest` | Fetch approved patterns |
| GET | `/api/v1/stats` | Network statistics |

**Base URL:** https://hivefence-api.seojoon-kim.workers.dev

## Why HiveFence?

Without protection:
- 91% injection attack success rate
- 84% data extraction success rate
- System prompts leaked on turn 1

(Source: [ZeroLeaks Security Assessment](https://x.com/NotLucknite/status/2017665998514475350))

With HiveFence:
- Real-time pattern blocking
- Collective immunity from the network
- Community-validated patterns (zero false positives)

## Links

- **Website:** https://hivefence.com
- **GitHub:** https://github.com/seojoonkim/hivefence
- **API Docs:** https://hivefence.com/docs

## License

MIT © 2026 Simon Kim (@seojoonkim)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
