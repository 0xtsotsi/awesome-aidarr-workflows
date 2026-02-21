# RequestHunt Workflow

**Status:** Active
**Date:** 2026-02-21
**Use Case:** Generate user demand research reports from real user feedback
**Source:** Adapted from OPC Skills (resciencelab/opc-skills)

## Overview

Collect and analyze real user feedback from Reddit, X (Twitter), and GitHub to generate comprehensive user demand research reports.

## ATLAS Alignment

| ATLAS Phase | Workflow Step |
|-------------|---------------|
| Architect | Define research scope and goals |
| Trace | Collect data from platforms |
| Link | Connect to RequestHunt API |
| Assemble | Analyze and generate report |
| Stress-test | Verify findings and sources |

## Trigger

This workflow is invoked when user mentions:
- Demand research, find feature requests
- Analyze user demand, RequestHunt queries
- User feedback analysis

## Prerequisites

Set API key in `~/.zshrc`:
```bash
export REQUESTHUNT_API_KEY="your_api_key"
```

Get key from: https://requesthunt.com/settings/api

**Quick Test:**
```bash
python3 scripts/get_usage.py
```

## Research Workflow

### Phase 1: Architect (Define Scope)

Clarify with user:
1. **Research Goal** - What domain to investigate?
2. **Specific Products** - Any competitors to focus on?
3. **Platform Preference** - reddit, x, github?
4. **Time Range** - How recent?
5. **Report Purpose** - Product planning / competitive analysis / market research?

### Phase 2: Trace (Collect Data)

```bash
# Trigger realtime scrape
python3 scripts/scrape_topic.py "ai-coding-assistant" --platforms reddit,x,github

# Search with expansion
python3 scripts/search_requests.py "code completion" --expand --limit 50

# List by topic
python3 scripts/list_requests.py --topic "ai-tools" --limit 100
```

### Phase 3: Link (API Connection)

**List Requests:**
```bash
python3 scripts/list_requests.py --limit 20
python3 scripts/list_requests.py --topic "ai-tools" --limit 10
python3 scripts/list_requests.py --platforms reddit,github
python3 scripts/list_requests.py --sortBy top --limit 20
```

**Search:**
```bash
python3 scripts/search_requests.py "authentication" --limit 20
python3 scripts/search_requests.py "oauth" --expand
```

**Get Topics:**
```bash
python3 scripts/get_topics.py
```

### Phase 4: Assemble (Generate Report)

```markdown
# [Topic] User Demand Research Report

## Overview
- Scope: ...
- Data Sources: Reddit (X), X (Y), GitHub (Z)

## Key Findings

### 1. Top Feature Requests
| Rank | Request | Sources | Quote |

### 2. Pain Points Analysis
- **Pain Point A**: ...

### 3. Competitive Comparison
| Feature | Product A | Product B |

### 4. Opportunities
- ...

## Methodology
Based on N real user feedbacks collected via RequestHunt...
```

### Phase 5: Stress-Test (Verify)

- Check source URLs are valid
- Verify data distribution across platforms
- Validate timestamp range

## API Info

- **Base URL**: https://requesthunt.com
- **Auth**: Bearer token (API key)
- **Rate Limits**:
  - Cached requests: 1000/month
  - Realtime requests: 500/month
- **Docs**: https://requesthunt.com/docs
