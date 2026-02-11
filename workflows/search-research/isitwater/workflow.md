# isitwater

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/johnnagro/isitwater/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/johnnagro/isitwater/SKILL.md)
> Category: Search & Research

---

## Description

Check if geographic coordinates are over water or land using the IsItWater API.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Check if geographic coordinates are over water or land using the IsItWater API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run isitwater`)
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
You are executing the isitwater workflow. Use the following context:

Description: Check if geographic coordinates are over water or land using the IsItWater API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: isitwater
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# IsItWater

Determine whether a latitude/longitude coordinate is over water using the IsItWater API.

## Setup

Before making API calls, check whether the user has an API key configured:

1. Check if `ISITWATER_API_KEY` is set in the environment.
2. If it is **not** set:
   - Inform the user: "You need an IsItWater API key. You can get one at https://isitwater.com"
   - Offer to help them sign up using the browser tool — navigate to https://isitwater.com, create an account, and generate an API key from the dashboard.
   - Once the user has a key, guide them to configure it in `~/.openclaw/openclaw.json`:

```json
{
  "skills": {
    "entries": {
      "isitwater": {
        "apiKey": "YOUR_API_KEY_HERE"
      }
    }
  }
}
```

   - Alternatively, the user can export the environment variable directly: `export ISITWATER_API_KEY=YOUR_API_KEY_HERE`

3. Once the key is available, proceed with the API calls below.

## Water Lookup

Check whether a coordinate is over water or land.

**Endpoint:** `GET https://api.isitwater.com/v1/locations/water`

**Headers:**

- `Authorization: Bearer $ISITWATER_API_KEY`

**Query Parameters:**

| Parameter | Type   | Required | Description                    |
|-----------|--------|----------|--------------------------------|
| `lat`     | number | yes      | Latitude, between -90 and 90   |
| `lon`     | number | yes      | Longitude, between -180 and 180 |

**Example curl:**

```bash
curl -s "https://api.isitwater.com/v1/locations/water?lat=41.7658&lon=-72.6734" \
  -H "Authorization: Bearer $ISITWATER_API_KEY"
```

**Example response (land):**

```json
{
  "request_id": "abc123",
  "water": false,
  "features": ["earth"],
  "latitude": "41.7658",
  "longitude": "-72.6734"
}
```

**Example response (water):**

```json
{
  "request_id": "def456",
  "water": true,
  "features": ["earth", "ocean"],
  "latitude": "36.0",
  "longitude": "-30.0"
}
```

**Response Fields:**

| Field        | Type     | Description                                                                                         |
|--------------|----------|-----------------------------------------------------------------------------------------------------|
| `request_id` | string   | Unique identifier for the request                                                                   |
| `water`      | boolean  | `true` if the coordinate is over water, `false` if over land                                        |
| `features`   | string[] | Geographic features at the point — e.g. `earth`, `ocean`, `lake`, `river`, `glacier`, `nature_reserve` |
| `latitude`   | string   | The latitude that was queried                                                                       |
| `longitude`  | string   | The longitude that was queried                                                                      |

**Cost:** 1 credit per lookup.

## Account Info

Check the user's account details and remaining credit balance.

**Endpoint:** `GET https://api.isitwater.com/v1/accounts/me`

**Headers:**

- `Authorization: Bearer $ISITWATER_API_KEY`

**Example curl:**

```bash
curl -s "https://api.isitwater.com/v1/accounts/me" \
  -H "Authorization: Bearer $ISITWATER_API_KEY"
```

**Response Fields:**

| Field                  | Type    | Description                          |
|------------------------|---------|--------------------------------------|
| `id`                   | string  | Account identifier                   |
| `name`                 | string  | Account name                         |
| `balance`              | number  | Remaining credits                    |
| `auto_recharge_enabled`| boolean | Whether auto-recharge is turned on   |

**Cost:** Free (no credits consumed).

## Error Handling

| Status Code | Meaning              | Description                                    |
|-------------|----------------------|------------------------------------------------|
| 200         | OK                   | Request succeeded                              |
| 400         | Bad Request          | Invalid latitude or longitude values           |
| 401         | Unauthorized         | Missing or invalid API key                     |
| 402         | Payment Required     | Account has no remaining credits               |

Error responses return a JSON body:

```json
{
  "error": "description of the problem"
}
```

## Tips

- Each water lookup costs **1 credit**. Use the Account Info endpoint to check the user's balance before making many requests.
- When the user provides a **place name** instead of coordinates (e.g. "Is the Sahara Desert water?"), geocode the location first to get lat/lon, then call the water lookup endpoint.
- The `features` array can contain **multiple overlapping values** for a single point — for example, a point might return both `lake` and `nature_reserve`.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
