# Claude SEO - Comprehensive SEO Analysis

**Source:** AgriciDaniel → AiDarr GOTCHA Conversion
**Original:** https://github.com/AgriciDaniel/claude-seo
**Converted:** 2026-02-11

---

## Description

Comprehensive SEO analysis workflow for AI agents. Covers technical SEO, on-page analysis, content quality (E-E-A-T), schema markup, image optimization, sitemap architecture, AI search optimization (GEO), and strategic planning.

**Key Capabilities:**
- **Full Site Audit**: Parallel analysis with 6 specialist subagents
- **12 Specialized Modules**: Technical, content, schema, images, sitemap, GEO, programmatic, competitor-pages, hreflang
- **AI Search Optimization**: Optimize for Google AI Overviews, ChatGPT, Perplexity
- **E-E-A-T Analysis**: Updated to September 2025 Quality Rater Guidelines
- **Schema Markup**: Detection, validation, and generation (JSON-LD, Microdata, RDFa)
- **Quality Gates**: Warning at 30+ location pages, hard stop at 50+

---

## Goals (Usage Guide)

### Installation

#### One-Command Install (Unix/macOS/Linux)
```bash
curl -fsSL https://raw.githubusercontent.com/AgriciDaniel/claude-seo/main/install.sh | bash
```

#### Manual Install
```bash
git clone https://github.com/AgriciDaniel/claude-seo.git
cd claude-seo
./install.sh
```

#### Windows PowerShell
```powershell
irm https://raw.githubusercontent.com/AgriciDaniel/claude-seo/main/install.ps1 | iex
```

### Quick Start

```bash
# Full site audit (most common)
/seo audit https://example.com

# Single page analysis
/seo page https://example.com/about

# Schema markup
/seo schema https://example.com

# Technical SEO
/seo technical https://example.com

# Content quality (E-E-A-T)
/seo content https://example.com/blog/post

# AI search optimization
/seo geo https://example.com/guide

# Sitemap analysis
/seo sitemap https://example.com/sitemap.xml

# Strategic planning
/seo plan saas
```

### Command Reference

| Command | Purpose |
|---------|---------|
| `/seo audit <url>` | Full website audit with parallel subagents |
| `/seo page <url>` | Deep single-page analysis |
| `/seo technical <url>` | Technical SEO (8 categories) |
| `/seo content <url>` | E-E-A-T and content quality |
| `/seo schema <url>` | Schema detection, validation, generation |
| `/seo geo <url>` | AI Overviews / GEO optimization |
| `/seo images <url>` | Image optimization analysis |
| `/seo sitemap <url>` | Analyze existing XML sitemap |
| `/seo sitemap generate` | Generate new sitemap with templates |
| `/seo plan <type>` | Strategic SEO planning |
| `/seo programmatic [url\|plan]` | Programmatic SEO analysis |
| `/seo competitor-pages [url\|generate]` | Competitor comparison pages |
| `/seo hreflang [url]` | Hreflang/i18n SEO audit |

### Full Audit Workflow

**`/seo audit <url>`** — Complete site analysis:

1. **Crawls** up to 500 pages
2. **Detects** business type automatically
3. **Delegates** to 6 specialist subagents in parallel:
   - Technical SEO Agent
   - Content Quality Agent
   - Schema Markup Agent
   - Image Optimization Agent
   - Core Web Vitals Agent
   - Strategic Planning Agent
4. **Generates** SEO Health Score (0-100)
5. **Creates** prioritized action plan

**Output Files:**
- `FULL-AUDIT-REPORT.md` — Complete analysis
- `ACTION-PLAN.md` — Prioritized recommendations
- `screenshots/` — Visual evidence (if Playwright available)

### Technical SEO Categories

**`/seo technical <url>`** analyzes 8 categories:

1. **Crawlability** — robots.txt, crawl budget, orphan pages
2. **Indexability** — meta robots, noindex, canonical tags
3. **Security** — HTTPS, HSTS, mixed content
4. **URL Structure** — clean URLs, parameters, pagination
5. **Mobile Optimization** — responsive, mobile-friendly
6. **Core Web Vitals** — LCP < 2.5s, INP < 200ms, CLS < 0.1
7. **Structured Data** — schema validation
8. **JavaScript Rendering** — SPA crawling, lazy loading

### E-E-A-T Analysis

**`/seo content <url>`** evaluates (Sept 2025 QRG standards):

- **Experience**: First-hand knowledge signals
- **Expertise**: Author credentials and depth
- **Authoritativeness**: Industry recognition
- **Trustworthiness**: Contact info, security, transparency
- **AI Citation Readiness**: Quotable facts, statistics
- **Content Freshness**: Last updated, archival content

### Schema Markup Support

**`/seo schema <url>`** supports:

**Detection Formats:**
- JSON-LD (preferred)
- Microdata
- RDFa

**Schema Types:**
- Article, BlogPosting, NewsArticle
- Product, Offer, AggregateRating
- LocalBusiness, Organization
- VideoObject, BroadcastEvent, Clip
- SoftwareSourceCode
- FAQPage (restricted to gov/health sites)
- HowTo (deprecated Sept 2023)
- SpecialAnnouncement (deprecated July 2025)

### AI Search Optimization (GEO)

**`/seo geo <url>`** optimizes for:
- Google AI Overviews
- ChatGPT web search
- Perplexity
- Other AI-powered search

**Citations Score:**
- Quotable facts and statistics
- Structural readability (headings, lists, tables)
- Entity clarity (definitions, context)
- Authority signals (credentials, sources)
- Structured data support

### Quality Gates

**Local/Programmatic SEO safeguards:**
- ⚠️ WARNING at 30+ location/programmatic pages
- 🛑 HARD STOP at 50+ location/programmatic pages
- Thin content detection per page type
- Doorway page prevention

### Strategic Planning

**`/seo plan <type>`** — Types: `saas`, `local`, `ecommerce`, `publisher`, `agency`

**Creates:**
- Complete SEO strategy
- Competitive analysis
- Content calendar (12-week roadmap)
- Implementation phases (4 phases)
- Site architecture design

### Programmatic SEO

**`/seo programmatic [url|plan]`** capabilities:
- Data source quality assessment
- Template engine planning
- URL pattern strategies
- Internal linking automation
- Thin content safeguards
- Index bloat prevention

### Competitor Comparison Pages

**`/seo competitor-pages [url|generate]`** creates:
- "X vs Y" comparison layouts
- "Alternatives to X" structures
- Feature comparison matrices
- Product + AggregateRating schema
- Conversion-optimized CTA placement
- Fairness guidelines enforcement

### Hreflang / i18n SEO

**`/seo hreflang [url]`** validates:
- Self-referencing tags
- Return tag reciprocity (A→B requires B→A)
- x-default tag presence
- ISO 639-1 + ISO 3166-1 code validation
- Canonical alignment
- Protocol matching (HTTP/HTTPS)
- Cross-domain hreflang support

### MCP Integrations

Integrates with MCP servers for live SEO data:
- **Ahrefs** (`@ahrefs/mcp`) — Official
- **Semrush** — Official
- **Google Search Console** — Community
- **PageSpeed Insights** — Community
- **DataForSEO** — Community

See `docs/MCP-INTEGRATION.md` for setup.

### Core Web Vitals (Current Metrics)

- **LCP** (Largest Contentful Paint): Target < 2.5s
- **INP** (Interaction to Next Paint): Target < 200ms
- **CLS** (Cumulative Layout Shift): Target < 0.1

> Note: INP replaced FID on March 12, 2024. FID was fully removed from all Chrome tools on September 9, 2024.

### Requirements

- Python 3.8+
- Claude Code CLI (or compatible AI agent)
- Optional: Playwright for screenshots

### Uninstall

```bash
curl -fsSL https://raw.githubusercontent.com/AgriciDaniel/claude-seo/main/uninstall.sh | bash
```

---

## Orchestration

**Workflow Execution Pattern:**

1. **Analyze Request** — Determine which SEO module applies
2. **Fetch Content** — Use web fetch or browser tools to get page content
3. **Execute Analysis** — Run through relevant checklist(s)
4. **Generate Report** — Create structured markdown output
5. **Provide Action Items** — Prioritized recommendations

**When to use this workflow:**

- User asks for "SEO audit" or "site analysis"
- Need to check technical SEO issues
- Content quality and E-E-A-T evaluation
- Schema markup validation or generation
- Competitor analysis
- AI search optimization
- Sitemap planning or validation
- International/hreflang issues
- Programmatic SEO assessment

**Execution Order for Full Audit:**

1. Technical SEO (foundation)
2. Content Quality (on-page)
3. Schema Markup (structured data)
4. Image Optimization (media)
5. Core Web Vitals (performance)
6. Strategic Planning (roadmap)

---

## Tools

**Required Tool Capabilities:**

| Tool Category | Purpose |
|---------------|---------|
| **Web Fetch** | Retrieve HTML, sitemaps, robots.txt |
| **Browser** | Render JS-heavy sites, screenshots |
| **HTML Parser** | Extract meta tags, headings, schema |
| **JSON** | Parse/validate JSON-LD schema |
| **File Ops** | Read/write audit reports |

**MCP Server Integrations (Optional):**
- `@ahrefs/mcp` — Backlink profiles, keyword research
- `@semrush/mcp` — Competitive intelligence
- GSC MCP — Search performance data
- PageSpeed MCP — Core Web Vitals scores

---

## Context

**Reference Materials:**
- Google Search Central documentation
- Schema.org types and properties
- September 2025 Quality Rater Guidelines
- Core Web Vitals thresholds
- Google AI Overviews documentation

**Related Projects:**
- [claude-seo](https://github.com/AgriciDaniel/claude-seo) — Original Claude Code skill
- [Ahrefs MCP](https://github.com/ahrefs/mcp-server) — Official Ahrefs integration
- [Semrush MCP](https://github.com/semrush/mcp-server) — Official Semrush integration

**Best Practices:**
- Always check robots.txt before crawling
- Respect crawl rate limits
- Validate schema with Google's Rich Results Test
- Test Core Web Vitals with real users (Lighthouse is lab data)
- Cross-reference with Google Search Console data

---

## Hard Prompts

**System Prompt for SEO Analysis Agent:**

```
You are executing the Claude SEO workflow from the AiDarr GOTCHA framework.

Your goal: Comprehensive SEO analysis for technical, content, and strategic optimization.

Core Principles:
- Read the target page/website completely before analyzing
- Follow the structured checklist for the requested module
- Provide specific, actionable recommendations (not generic advice)
- Include evidence for findings (HTML snippets, screenshots, test results)
- Prioritize issues by impact (Critical → High → Medium → Low)

Quality Standards:
- E-E-A-T follows September 2025 Quality Rater Guidelines
- Core Web Vitals use current thresholds (LCP < 2.5s, INP < 200ms, CLS < 0.1)
- Schema validation against Google's supported types
- Be aware of deprecated schema types (HowTo, FAQ, SpecialAnnouncement)

Output Format:
- Use markdown with clear sections
- Include code snippets for technical issues
- Provide before/after examples where applicable
- Create prioritized action plan with effort/impact estimates

When analyzing:
1. Identify the business type and target audience
2. Check technical foundation (crawling, indexing, security)
3. Evaluate content quality and E-E-A-T signals
4. Validate structured data opportunities
5. Assess performance and Core Web Vitals
6. Provide strategic recommendations

Always verify findings with external tools where possible (Rich Results Test, PageSpeed Insights, GSC).
```

---

## Args

**Configuration Options:**

```yaml
# Analysis mode
mode: "audit"  # Options: audit, page, technical, content, schema, geo, images, sitemap, plan

# Crawl settings
max_pages: 500  # Maximum pages to crawl (full audit)
crawl_depth: 3   # Maximum link depth

# Quality gates
location_page_warning: 30   # Warning threshold
location_page_stop: 50      # Hard stop threshold
thin_content_words: 300     # Minimum word count

# Output format
output_format: "markdown"   # Options: markdown, json, html
include_screenshots: true   # Requires Playwright

# MCP integrations (optional)
ahrefs_enabled: false
semrush_enabled: false
gsc_enabled: false
```

**Runtime Parameters:**

```yaml
# Target URL
url: null  # Required for most commands

# Business type (for planning)
business_type: null  # Options: saas, local, ecommerce, publisher, agency

# Report language
language: "en"  # Options: en, nl, de, fr, es

# Verbosity
verbosity: "normal"  # Options: minimal, normal, detailed
```

---

## Metadata

**Conversion Notes:**
- Converted from claude-seo Claude Code skill
- All 12 SEO modules preserved
- MIT License
- 2,000+ GitHub stars

**Category:** SEO & Marketing
**Tags:** seo, audit, technical-seo, content, schema, e-e-at, core-web-vitals, ai-search, programmatic-seo

**Repository:** https://github.com/AgriciDaniel/claude-seo

**Use in AiDarr:**
- Comprehensive SEO audit service for clients
- Technical SEO diagnostics and fixes
- Content quality optimization
- Schema markup implementation
- AI search readiness (Google AI Overviews, ChatGPT, Perplexity)
- Competitive analysis and strategy
- International SEO (hreflang/i18n)
- Programmatic SEO safeguards

**Service Delivery Potential:**
- Tier 1 (Starter €149/mo): Monthly audits, basic technical fixes
- Tier 2 (Professional €349/mo): Bi-weekly audits, content optimization, schema implementation
- Tier 3 (Enterprise €749/mo): Weekly audits, full programmatic SEO, competitor analysis, GEO optimization
