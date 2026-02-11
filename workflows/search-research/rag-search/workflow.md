# rag-search

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/loda666/rag-search/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/loda666/rag-search/SKILL.md)
> Category: Search & Research

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
**Trigger:** User-invocable (via `aidarr run rag-search`)
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
You are executing the rag-search workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: rag-search
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# rag-search

Minimal RAG search skill for backend retrieval.

## ⚠️ Important

**This skill is intended to be used as a backend retrieval component and should not be invoked directly by end users.**

Use `occupational_health_qa` or `occupational_health_report_writer` for direct user requests.

## Usage

```
你：调用 rag-search，查询"GBZ 2.1-2019 苯 职业接触限值"
```

## Returns

Returns structured search results with:
- `content`: Original text from the document
- `source`: File name / standard number
- `clause`: Clause number (if available)
- `regulation_level`: Regulation level (国家法律/国家标准/行业标准/etc)
- `score`: Relevance score (0-1)

## Example Response

```json
{
  "results": [
    {
      "content": "苯的时间加权平均容许浓度（PC-TWA）为6 mg/m³...",
      "source": "GBZ 2.1-2019.pdf",
      "clause": "第4.1条",
      "regulation_level": "国家标准",
      "score": 0.93
    }
  ]
}
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
