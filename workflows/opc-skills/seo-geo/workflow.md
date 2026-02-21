# SEO/GEO Optimization Workflow

**Status:** Active
**Date:** 2026-02-21
**Use Case:** Optimize content for both traditional SEO and AI-driven Generative Engine Optimization (GEO)
**Source:** Adapted from OPC Skills (resciencelab/opc-skills)

## Overview

This workflow optimizes web content for dual visibility:
1. **SEO** - Traditional search engine ranking (Google, Bing)
2. **GEO** - AI engine citations (ChatGPT, Perplexity, Claude, Copilot)

Based on Princeton GEO research: "Content optimization for Generative Engines"

## ATLAS Alignment

| ATLAS Phase | Workflow Step |
|-------------|---------------|
| Architect | Audit current state, identify target keywords |
| Trace | Extract existing meta tags, schema markup |
| Link | Map to platform-specific algorithms |
| Assemble | Implement meta tags, schema, content structure |
| Stress-test | Validate with tools, monitor indexing |

## GOTCHA Integration

| GOTCHA Component | Application |
|------------------|-------------|
| Goal | Improve search visibility and AI citations |
| Obstacles | Missing meta tags, blocked bots, no schema |
| Tactics | GEO methods, platform optimization |
| Constraints | Character limits, platform requirements |
| Helpers | WebSearch, validation tools |
| Alternatives | Manual vs automated optimization |

## Trigger

This workflow is invoked when:
- User requests SEO optimization
- User wants AI search engine visibility (ChatGPT, Perplexity, Claude, Copilot)
- New content page needs optimization
- Existing content needs GEO audit
- Keywords mentioned: SEO, GEO, search visibility, AI visibility, ranking, indexing, JSON-LD, meta tags

## Prerequisites

- Target URL or content file identified
- Write access to content/code
- For new content: brainstorm session completed

## Workflow Steps

### Phase 1: Architect (Audit & Plan)

**Goal:** Understand current state and target keywords

```bash
# Define target
TARGET_URL="https://example.com/page"
PRIMARY_KEYWORD="your primary keyword"
SECONDARY_KEYWORDS=("keyword 2" "keyword 3" "keyword 4")
```

**Analysis Checklist:**
- [ ] What question does this content answer?
- [ ] Who is the target audience?
- [ ] What AI engines matter most? (ChatGPT, Perplexity, Claude, Copilot)
- [ ] Current ranking status?

### Phase 2: Trace (Extract Current State)

**Meta Tag Audit:**
```bash
curl -sL "$TARGET_URL" | grep -E "<title>|<meta name=\"description\"|<meta property=\"og:|application/ld\+json"
```

**Robots.txt Check:**
```bash
curl -s "${TARGET_URL%%/*}/robots.txt"
```

**Sitemap Check:**
```bash
curl -s "${TARGET_URL%%/*}/sitemap.xml" | head -50
```

### Phase 3: Link (Platform Requirements)

| Platform | Key Factors | Priority |
|----------|-------------|----------|
| ChatGPT | Branded domain, 30-day freshness, backlinks | High |
| Perplexity | PerplexityBot allowed, FAQ schema, PDFs | High |
| Google SGE | E-E-A-T, structured data, citations | Medium |
| Copilot | Bing indexing, page speed <2s | Medium |
| Claude | Brave indexing, factual density | High |

### Phase 4: Assemble (Implement)

**Meta Tags Template:**
```html
<title>{Primary Keyword} - {Brand} | {Secondary Keyword}</title>
<meta name="description" content="{150-160 chars with keyword}">
<meta name="keywords" content="{keyword1}, {keyword2}, {keyword3}">

<!-- Open Graph -->
<meta property="og:title" content="{Title}">
<meta property="og:description" content="{Description}">
<meta property="og:image" content="{Image URL 1200x630}">
<meta property="og:url" content="{Canonical URL}">
```

**robots.txt for AI bots:**
```
User-agent: ChatGPT
Allow: /

User-agent: PerplexityBot
Allow: /

User-agent: Claude
Allow: /

User-agent: GPTBot
Allow: /
```

**FAQPage Schema (GEO boost):**
```json
{
  "@context": "https://schema.org",
  "@type": "FAQPage",
  "mainEntity": [{
    "@type": "Question",
    "name": "[Question matching user intent]",
    "acceptedAnswer": {
      "@type": "Answer",
      "text": "[Concise answer with statistics]"
    }
  }]
}
```

### Phase 5: Stress-Test (Validate)

**Schema Validation:**
```bash
open "https://search.google.com/test/rich-results?url={encoded_url}"
open "https://validator.schema.org/?url={encoded_url}"
```

**Indexing Check:**
```bash
open "https://www.google.com/search?q=site:{domain}"
open "https://www.bing.com/search?q=site:{domain}"
```

## GEO Optimization Methods

Based on Princeton research (visibility boost):

| Method | Boost | Implementation |
|--------|-------|----------------|
| Cite Sources | +40% | Add authoritative citations |
| Statistics | +37% | Include specific numbers |
| Quotations | +30% | Add expert quotes |
| Authoritative Tone | +25% | Use confident language |
| Easy-to-understand | +20% | Simplify concepts |
| Technical Terms | +18% | Include domain terminology |
| Unique Words | +15% | Vocabulary diversity |
| Fluency | +15-30% | Improve readability |
| ~~Keyword Stuffing~~ | **-10%** | **AVOID** |

## Report Template

```markdown
## SEO/GEO Optimization Report

### Current Status
- Meta Tags: ✅/❌
- Schema Markup: ✅/❌
- AI Bot Access: ✅/❌
- Mobile Friendly: ✅/❌
- Page Speed: X seconds

### Recommendations
1. [Priority 1 action]
2. [Priority 2 action]
3. [Priority 3 action]

### GEO Optimizations Applied
- [ ] FAQPage schema added
- [ ] Statistics included
- [ ] Citations added
- [ ] Answer-first structure
```

## References

- [references/platform-algorithms.md](./references/platform-algorithms.md) - Detailed ranking factors
- [references/geo-research.md](./references/geo-research.md) - Princeton GEO research
- [references/schema-templates.md](./references/schema-templates.md) - JSON-LD templates
- [references/seo-checklist.md](./references/seo-checklist.md) - Complete audit checklist
