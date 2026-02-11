# seo-competitor-analysis

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/qqyule/seo-competitor-analysis/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/qqyule/seo-competitor-analysis/SKILL.md)
> Category: Marketing & Sales

---

## Description

Perform deep SEO competitor analysis, including keyword research, backlink checking, and content strategy mapping. Use when the user wants to analyze a website's competitors or improve their own SEO ranking by studying the competition.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Perform deep SEO competitor analysis, including keyword research, backlink checking, and content strategy mapping. Use when the user wants to analyze a website's competitors or improve their own SEO ranking by studying the competition.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run seo-competitor-analysis`)
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
You are executing the seo-competitor-analysis workflow. Use the following context:

Description: Perform deep SEO competitor analysis, including keyword research, backlink checking, and content strategy mapping. Use when the user wants to analyze a website's competitors or improve their own SEO ranking by studying the competition.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: seo-competitor-analysis
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# SEO Competitor Analysis Skill

This skill automates the process of identifying and analyzing SEO competitors to inform content and ranking strategies.

## Workflow

1. **Identify Competitors**: If not provided, search for the target domain and identify top-ranking sites for similar keywords.
2. **Analyze Keywords**: Use `web_search` to find ranking keywords and search volume (if available via snippets).
3. **Content Gap Analysis**: Compare the user's content with competitors to identify missing topics.
4. **Report Generation**: Summarize findings into a structured report.

## Tools to Use

- `web_search`: To find competitors and their ranking content.
- `web_fetch`: To extract content from competitor pages for deep analysis.
- `browser`: For complex pages that require JavaScript or manual navigation patterns.

## Scripts

- `scripts/competitor_finder.py`: (Optional) Logic to automate the discovery of competitors using search APIs.

## References

- `references/seo_metrics_guide.md`: Definition of SEO terms and how to interpret them.
- `references/report_template.md`: A standard structure for the final SEO analysis report.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
