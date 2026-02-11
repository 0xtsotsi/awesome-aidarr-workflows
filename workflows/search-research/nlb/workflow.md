# nlb

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kk17/nlb/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kk17/nlb/SKILL.md)
> Category: Search & Research

---

## Description

check loans and search resources from the National Library Board of Singapore

**Homepage:** https://www.nlb.gov.sg
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
check loans and search resources from the National Library Board of Singapore

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run nlb`)
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
You are executing the nlb workflow. Use the following context:

Description: check loans and search resources from the National Library Board of Singapore

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: nlb
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: https://www.nlb.gov.sg
```

---

## Original Skill Content



# NLB Skill

## Login to NLB

1. Open https://signin.nlb.gov.sg/authenticate/login
2. Use user myLibrary username and password to login

## Check Loans(requires login)

1. Open https://www.nlb.gov.sg/mylibrary/loans
2. Check "Current" Tab to see borrowed items and due dates
3. Check "Overdue" Tab to see past borrowed items

## Check Recommendations(requires login)

1. Open https://www.nlb.gov.sg/mylibrary/Home

## Search Resources

1. URL Encode the search query
2. Open search result page: https://catalogue.nlb.gov.sg/search?query={url_encoded_query}
   Optional URL parameter filters:
   - &universalLimiterIds=at_library (to filter to only items available at libraries)
   - &pageNum=0 (to specify page number, starting from 0)
   - &viewType=grid (to view results in grid format)
   - &materialTypeIds=1 (to filter to books only)
   - &collectionIds={collection_ids} (to filter by specific collections, see below for details)
   - &locationIds={location_ids} (to filter by specific libraries, see below for details)
   - languageIds={language_ids} (to filter by specific languages, chi: Chinese, eng: English, mal: Malay, tam: Tamil)

### Collection Id Mappings:
| Collection Name                      | Collection Id |
| ------------------------------------ | ------------- |
| Early Literacy 4-6                   | 7             |
| Junior Picture Book                  | 11            |
| Junior                               | 9             |
| Early Literacy Accessible Collection | 55            |
| Junior Simple Fiction                | 12            |
| Junior Accessible Collection         | 8             |
| Adult                                | 3             |

### Location Id Mappings:
| Library Name      | Location ID |
| ----------------- | ----------- |
| Toa Payoh Library | 23          |
| Bishan Library    | 6           |
| Central Library   | 29          |


### Example

For search query "BookLife readers", filtering to items book only, available at Toa Payoh Library, in Junior Picture Book and Junior collections, viewing first page in grid format:
https://catalogue.nlb.gov.sg/search?query=BookLife%20readers&pageNum=0&locationIds=23&universalLimiterIds=at_library&collectionIds=11,9,7&viewType=grid&materialTypeIds=1

## Open Search Crad Page
1. Click the rearch result link to open the search result page in browser
Search Card Page Example:
https://catalogue.nlb.gov.sg/search/card?id=127ebe36-bad7-566c-8d81-3a32379254ad&entityType=FormatGroup


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
