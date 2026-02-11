# twenty-crm

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jhumanj/twenty-crm/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jhumanj/twenty-crm/SKILL.md)
> Category: Marketing & Sales

---

## Description

Interact with Twenty CRM (self-hosted) via REST/GraphQL.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Interact with Twenty CRM (self-hosted) via REST/GraphQL.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run twenty-crm`)
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
You are executing the twenty-crm workflow. Use the following context:

Description: Interact with Twenty CRM (self-hosted) via REST/GraphQL.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: twenty-crm
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Twenty CRM

Interact with your self-hosted Twenty instance via REST and GraphQL.

## Config

Create `config/twenty.env` (example at `config/twenty.env.example`):

- `TWENTY_BASE_URL` (e.g. `https://crm.example.com` or `http://localhost:3000`)
- `TWENTY_API_KEY` (Bearer token)

Scripts load this file automatically.

## Commands

### Low-level helpers

- REST GET: `skills/twenty-crm/scripts/twenty-rest-get.sh "/companies" 'filter={"name":{"ilike":"%acme%"}}&limit=10'`
- REST POST: `skills/twenty-crm/scripts/twenty-rest-post.sh "/companies" '{"name":"Acme"}'`
- REST PATCH: `skills/twenty-crm/scripts/twenty-rest-patch.sh "/companies/<id>" '{"employees":550}'`
- REST DELETE: `skills/twenty-crm/scripts/twenty-rest-delete.sh "/companies/<id>"`

- GraphQL: `skills/twenty-crm/scripts/twenty-graphql.sh 'query { companies(limit: 5) { totalCount } }'`

### Common objects (examples)

- Create company: `skills/twenty-crm/scripts/twenty-create-company.sh "Acme" "acme.com" 500`
- Find companies by name: `skills/twenty-crm/scripts/twenty-find-companies.sh "acme" 10`

## Notes

- Twenty supports both REST (`/rest/...`) and GraphQL (`/graphql`).
- Object names/endpoints can differ depending on your workspace metadata and Twenty version.
- Auth tokens can be short-lived depending on your setup; refresh if you get `401`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
