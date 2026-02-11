# straker-verify

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/indy-at-straker/straker-verify/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/indy-at-straker/straker-verify/SKILL.md)
> Category: AI & LLMs

---

## Description

Professional AI-powered translation with optional human verification. Supports 100+ languages. Quality boost for existing translations. Enterprise-grade security and privacy by straker.ai.

**Homepage:** https://straker.ai
**Repository:** https://github.com/strakergroup/straker-verify-openclaw
**Version:** 1.0.0

**Tags:** translation, localization, i18n, internationalization, l10n, language, translate, multilingual, quality-assurance, human-verification, ai-translation, straker, verify, enterprise, professional, api, nlp, language-services, content-localization, translation-management

---

## GOTCHA Framework

### G - Goals
Professional AI-powered translation with optional human verification. Supports 100+ languages. Quality boost for existing translations. Enterprise-grade security and privacy by straker.ai.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run straker-verify`)
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
You are executing the straker-verify workflow. Use the following context:

Description: Professional AI-powered translation with optional human verification. Supports 100+ languages. Quality boost for existing translations. Enterprise-grade security and privacy by straker.ai.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: straker-verify
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: https://straker.ai
```

---

## Original Skill Content



# Straker Verify - AI Translation & Human Review

Professional translation, quality evaluation, and human verification services by [Straker.ai](https://straker.ai).

## Features

- **AI Translation**: Translate content to 100+ languages with enterprise-grade accuracy
- **Quality Boost**: AI-powered enhancement for existing translations
- **Human Verification**: Professional human review for critical content
- **File Support**: Documents, text files, and more
- **Project Management**: Track translation projects from submission to delivery

## Quick Start

1. Get your API key from [Straker.ai](https://straker.ai)
2. Set the environment variable: `STRAKER_VERIFY_API_KEY=your-key`
3. Ask your AI assistant: "Translate 'Hello world' to French"

## API Reference

**Base URL:** `https://api-verify.straker.ai`

### Authentication

All requests (except `/languages`) require Bearer token authentication:

```bash
curl -H "Authorization: Bearer $STRAKER_VERIFY_API_KEY" https://api-verify.straker.ai/endpoint
```

### Get Available Languages

```bash
curl https://api-verify.straker.ai/languages
```

Returns a list of supported language pairs with UUIDs for use in other endpoints.

### Create Translation Project

```bash
curl -X POST https://api-verify.straker.ai/project \
  -H "Authorization: Bearer $STRAKER_VERIFY_API_KEY" \
  -F "files=@document.txt" \
  -F "languages=<language-uuid>" \
  -F "title=My Translation Project" \
  -F "confirmation_required=true"
```

### Confirm Project

Required when `confirmation_required=true`:

```bash
curl -X POST https://api-verify.straker.ai/project/confirm \
  -H "Authorization: Bearer $STRAKER_VERIFY_API_KEY" \
  -H "Content-Type: application/x-www-form-urlencoded" \
  -d "project_id=<project-uuid>"
```

### Check Project Status

```bash
curl https://api-verify.straker.ai/project/<project-uuid> \
  -H "Authorization: Bearer $STRAKER_VERIFY_API_KEY"
```

### Download Completed Files

```bash
curl https://api-verify.straker.ai/project/<project-uuid>/download \
  -H "Authorization: Bearer $STRAKER_VERIFY_API_KEY" \
  -o translations.zip
```

### AI Quality Boost

Enhance existing translations with AI:

```bash
curl -X POST https://api-verify.straker.ai/quality-boost \
  -H "Authorization: Bearer $STRAKER_VERIFY_API_KEY" \
  -F "files=@source.txt" \
  -F "language=<language-uuid>"
```

### Human Verification

Add professional human review to translations:

```bash
curl -X POST https://api-verify.straker.ai/human-verify \
  -H "Authorization: Bearer $STRAKER_VERIFY_API_KEY" \
  -F "files=@translated.txt" \
  -F "language=<language-uuid>"
```

## Response Format

**Success:**
```json
{
  "success": true,
  "data": { ... }
}
```

**Error:**
```json
{
  "success": false,
  "error": "Error message"
}
```

## Example Prompts

- "What languages can I translate to?"
- "Translate this text to Spanish: Hello, how are you?"
- "Create a translation project for my document"
- "Check the status of my translation project"
- "Run a quality boost on this French translation"
- "Add human verification to my German translation"

## Support

- Website: [straker.ai](https://straker.ai)
- API Docs: [api-verify.straker.ai/docs](https://api-verify.straker.ai/docs)

## Environment

The API key is available as `$STRAKER_VERIFY_API_KEY` environment variable.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
