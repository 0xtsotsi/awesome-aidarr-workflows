# strykr-qa-bot

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/nextfrontierbuilds/strykr-qa-bot/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/nextfrontierbuilds/strykr-qa-bot/SKILL.md)
> Category: Web & Frontend Development

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run strykr-qa-bot`)
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
You are executing the strykr-qa-bot workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: strykr-qa-bot
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# strykr-qa-bot

QA automation skill for testing Strykr (https://app.strykr.ai).

## What It Does

Automated testing for the Strykr AI finance dashboard:
- Pre-built test suites for all pages
- Signal card validation
- AI response quality checks
- PRISM API health monitoring
- Known issue tracking

## When To Use

- Testing Strykr after deployments
- Regression testing
- Monitoring site health
- Validating new features

## Usage

### Run All Tests
```bash
cd /path/to/strykr-qa-bot
npm test
```

### Run Specific Suite
```bash
npm run test:homepage
npm run test:crypto
npm run test:stocks
npm run test:news
npm run test:events
npm run test:ai-chat
```

### Quick Smoke Test
```bash
npm run smoke
```

### Programmatic Usage
```typescript
import { StrykrQABot } from 'strykr-qa-bot';

const qa = new StrykrQABot({
  baseUrl: 'https://app.strykr.ai'
});

// Run all suites
const results = await qa.runAll();

// Check specific assertions
await qa.expectSignalCard({ hasPrice: true, hasChart: true });
await qa.expectAIResponse({ minLength: 200 });

// Health check API
const health = await qa.checkPrismEndpoints();

// Generate report
const report = qa.generateReport();
```

## Test Suites

| Suite | Tests | Notes |
|-------|-------|-------|
| homepage | Navigation, widgets, status | Entry point |
| crypto-signals | Filters, cards, actions | Has known modal issue |
| stock-signals | Asset filters, actions | Stocks/ETFs/Forex |
| news | Routing, categories | Known direct URL issue |
| events | Impact filters, times | Known direct URL issue |
| ai-chat | Input, responses | Quality validation |

## Known Issues Tracked

1. **details-modal-empty** (High) - Modal opens but content empty
2. **direct-url-blank-news** (Medium) - /news blank on direct nav
3. **direct-url-blank-events** (Medium) - /economic-events blank
4. **events-widget-race-condition** (Low) - Intermittent widget load

## Configuration

Edit `strykr-qa.yaml`:
```yaml
baseUrl: https://app.strykr.ai
browser:
  headless: false
  timeout: 30000
```

## Dependencies

- [web-qa-bot](https://github.com/NextFrontierBuilds/web-qa-bot) (peer dependency)

## Output

Test results with:
- Pass/Fail/Known-issue status
- Screenshots at each step
- Console error capture
- Timing metrics
- Markdown report

## Author

Next Frontier (@NextXFrontier)

## Links

- [GitHub](https://github.com/NextFrontierBuilds/strykr-qa-bot)
- [Strykr](https://app.strykr.ai)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
