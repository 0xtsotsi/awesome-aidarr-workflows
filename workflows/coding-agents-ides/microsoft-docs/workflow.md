# microsoft-docs

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/pdebruin/microsoft-docs/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/pdebruin/microsoft-docs/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Query official Microsoft documentation to understand concepts, find tutorials, and learn how services work. Use for Azure, .NET, Microsoft 365, Windows, Power Platform, and all Microsoft technologies. Get accurate, current information from learn.microsoft.com and other official Microsoft websites—architecture overviews, quickstarts, configuration guides, limits, and best practices.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Query official Microsoft documentation to understand concepts, find tutorials, and learn how services work. Use for Azure, .NET, Microsoft 365, Windows, Power Platform, and all Microsoft technologies. Get accurate, current information from learn.microsoft.com and other official Microsoft websites—architecture overviews, quickstarts, configuration guides, limits, and best practices.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run microsoft-docs`)
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
You are executing the microsoft-docs workflow. Use the following context:

Description: Query official Microsoft documentation to understand concepts, find tutorials, and learn how services work. Use for Azure, .NET, Microsoft 365, Windows, Power Platform, and all Microsoft technologies. Get accurate, current information from learn.microsoft.com and other official Microsoft websites—architecture overviews, quickstarts, configuration guides, limits, and best practices.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: microsoft-docs
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Microsoft Docs

## Tools

| Tool | Use For |
|------|---------|
| `microsoft_docs_search` | Find documentation—concepts, guides, tutorials, configuration |
| `microsoft_docs_fetch` | Get full page content (when search excerpts aren't enough) |

## When to Use

- **Understanding concepts** — "How does Cosmos DB partitioning work?"
- **Learning a service** — "Azure Functions overview", "Container Apps architecture"
- **Finding tutorials** — "quickstart", "getting started", "step-by-step"
- **Configuration options** — "App Service configuration settings"
- **Limits & quotas** — "Azure OpenAI rate limits", "Service Bus quotas"
- **Best practices** — "Azure security best practices"

## Query Effectiveness

Good queries are specific:

```
# ❌ Too broad
"Azure Functions"

# ✅ Specific
"Azure Functions Python v2 programming model"
"Cosmos DB partition key design best practices"
"Container Apps scaling rules KEDA"
```

Include context:
- **Version** when relevant (`.NET 8`, `EF Core 8`)
- **Task intent** (`quickstart`, `tutorial`, `overview`, `limits`)
- **Platform** for multi-platform docs (`Linux`, `Windows`)

## When to Fetch Full Page

Fetch after search when:
- **Tutorials** — need complete step-by-step instructions
- **Configuration guides** — need all options listed
- **Deep dives** — user wants comprehensive coverage
- **Search excerpt is cut off** — full context needed

## Why Use This

- **Accuracy** — live docs, not training data that may be outdated
- **Completeness** — tutorials have all steps, not fragments
- **Authority** — official Microsoft documentation

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
