# productboard-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/robertoamoreno/productboard-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/robertoamoreno/productboard-search/SKILL.md)
> Category: Search & Research

---

## Description

Search and explore ProductBoard features, products, and feedback

**Homepage:** https://github.com/robertoamoreno/openclaw-productboard
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Search and explore ProductBoard features, products, and feedback

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run productboard-search`)
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
You are executing the productboard-search workflow. Use the following context:

Description: Search and explore ProductBoard features, products, and feedback

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: productboard-search
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: https://github.com/robertoamoreno/openclaw-productboard
```

---

## Original Skill Content



# ProductBoard Search Skill

Search and explore your ProductBoard workspace to find features, products, components, and customer feedback.

## Available Tools

- `pb_search` - Global search across all ProductBoard entities
- `pb_feature_list` - List features with filters
- `pb_feature_get` - Get detailed feature information
- `pb_feature_search` - Search features by name/description
- `pb_product_list` - List all products
- `pb_product_get` - Get product details with components
- `pb_product_hierarchy` - View full product/component tree
- `pb_note_list` - List customer feedback notes

## Search Strategies

### Finding Features

1. **By keyword**: Use `pb_feature_search` with a query term
2. **By product**: Use `pb_feature_list` with `productId` filter
3. **By status**: Use `pb_feature_list` with `status` filter (new, in-progress, shipped, archived)
4. **By component**: Use `pb_feature_list` with `componentId` filter

### Understanding Structure

1. Start with `pb_product_hierarchy` to see the complete workspace organization
2. Use `pb_product_get` to explore a specific product and its components
3. Filter features by product or component to narrow down results

### Finding Customer Feedback

1. Use `pb_note_list` to see recent feedback
2. Filter by date range using `createdFrom` and `createdTo`
3. Use `pb_search` with type `note` to find specific feedback

## Example Queries

**User**: "Find all features related to authentication"
**Action**: Use `pb_feature_search` with query "authentication"

**User**: "What features are currently in progress?"
**Action**: Use `pb_feature_list` with status "in-progress"

**User**: "Show me the product structure"
**Action**: Use `pb_product_hierarchy` to get the full tree

**User**: "Find customer feedback about performance"
**Action**: Use `pb_search` with query "performance" and type "note"

## Tips

- Start broad with `pb_search`, then narrow down with specific tools
- Use `pb_product_hierarchy` first when exploring an unfamiliar workspace
- The search is case-insensitive and matches partial words
- Results include direct links to ProductBoard for quick access

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
