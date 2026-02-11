# swiss-phone-directory

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/xenofex7/swiss-phone-directory/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/xenofex7/swiss-phone-directory/SKILL.md)
> Category: Transportation

---

## Description

Swiss phone directory lookup via search.ch API. Search for businesses, people, or reverse-lookup phone numbers. Use when: (1) finding contact details for Swiss companies or people, (2) looking up addresses by name or phone number, (3) reverse phone number lookup, (4) finding business categories. Requires SEARCHCH_API_KEY.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Swiss phone directory lookup via search.ch API. Search for businesses, people, or reverse-lookup phone numbers. Use when: (1) finding contact details for Swiss companies or people, (2) looking up addresses by name or phone number, (3) reverse phone number lookup, (4) finding business categories. Requires SEARCHCH_API_KEY.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run swiss-phone-directory`)
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
You are executing the swiss-phone-directory workflow. Use the following context:

Description: Swiss phone directory lookup via search.ch API. Search for businesses, people, or reverse-lookup phone numbers. Use when: (1) finding contact details for Swiss companies or people, (2) looking up addresses by name or phone number, (3) reverse phone number lookup, (4) finding business categories. Requires SEARCHCH_API_KEY.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: swiss-phone-directory
category: Transportation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Swiss Phone Directory Skill

Search the Swiss phone directory (search.ch) for businesses, people, and phone numbers.

## Quick Start

```bash
# Search for a business
python3 scripts/searchch.py search "Migros" --location "Zürich"

# Search for a person
python3 scripts/searchch.py search "Müller Hans" --type person

# Reverse phone number lookup
python3 scripts/searchch.py search "+41442345678"

# Business-only search
python3 scripts/searchch.py search "Restaurant" --location "Bern" --type business --limit 5
```

## Commands

### search
Search for businesses, people, or phone numbers.

```bash
python3 scripts/searchch.py search <query> [options]

Options:
  --location, -l    City, ZIP, street, or canton (e.g., "Zürich", "8000", "ZH")
  --type, -t        Filter: "business", "person", or "all" (default: all)
  --limit, -n       Max results (default: 10, max: 200)
  --lang            Output language: de, fr, it, en (default: de)
```

### Examples

```bash
# Find restaurants in Rapperswil
python3 scripts/searchch.py search "Restaurant" -l "Rupperswil" -t business -n 5

# Find a person by name
python3 scripts/searchch.py search "Meier Peter" -l "Zürich" -t person

# Reverse lookup a phone number
python3 scripts/searchch.py search "044 123 45 67"

# Search with canton abbreviation
python3 scripts/searchch.py search "Bäckerei" -l "SG"
```

## Output Format

Results include (when available):
- **Name** - Business or person name
- **Type** - Organisation or Person
- **Address** - Street, ZIP, city, canton
- **Phone** - Phone number(s)
- **Fax** - Fax number
- **Email** - Email address
- **Website** - Website URL
- **Categories** - Business categories

## Configuration

See [references/configuration.md](references/configuration.md) for setup.

Required: `SEARCHCH_API_KEY` environment variable.

## API Reference

- Base URL: `https://search.ch/tel/api/`
- Rate limits: Depend on API key tier
- Full docs: https://search.ch/tel/api/help.en.html

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
