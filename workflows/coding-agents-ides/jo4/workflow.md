# jo4

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/anandrathnas/jo4/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/anandrathnas/jo4/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

URL shortener, QR code generator, and link analytics API. Create short links, generate QR codes, and track click analytics.

**Homepage:** https://jo4.io
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
URL shortener, QR code generator, and link analytics API. Create short links, generate QR codes, and track click analytics.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run jo4`)
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
You are executing the jo4 workflow. Use the following context:

Description: URL shortener, QR code generator, and link analytics API. Create short links, generate QR codes, and track click analytics.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: jo4
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: https://jo4.io
```

---

## Original Skill Content



# Jo4 - URL Shortener & Analytics API

Jo4 is a modern URL shortening service with QR code generation and detailed link analytics.

## Authentication

All protected endpoints require an API key. Set your API key as an environment variable:

```bash
export JO4_API_KEY="your-api-key"
```

Get your API key from: https://jo4.io/api-keys

## API Base URL

```
https://jo4-api.jo4.io/api/v1
```

## Endpoints

### Create Short URL (Authenticated)

```bash
curl -X POST "https://jo4-api.jo4.io/api/v1/protected/url" \
  -H "X-API-Key: $JO4_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "longUrl": "https://example.com/very-long-url",
    "title": "My Link"
  }'
```

**Request Body:**
- `longUrl` (required) - The destination URL (max 2048 chars)
- `title` (optional) - Link title (max 200 chars)
- `description` (optional) - Link description (max 500 chars)
- `shortUrl` (optional) - Custom alias (max 16 chars, alphanumeric/hyphen/underscore)
- `expirationTime` (optional) - Unix timestamp for link expiration
- `passwordProtected` (optional) - Boolean to enable password protection
- `password` (optional) - Password if protected (4-128 chars)

**UTM Parameters:**
- `utmSource`, `utmMedium`, `utmCampaign`, `utmTerm`, `utmContent`

**Response:**
```json
{
  "response": {
    "id": 123,
    "slug": "abc123",
    "shortUrl": "abc123",
    "fullShortUrl": "https://jo4.io/a/abc123",
    "longUrl": "https://example.com/very-long-url",
    "title": "My Link",
    "qrCodeUrl": "https://jo4.io/qr/abc123"
  }
}
```

### Create Anonymous Short URL (No Auth Required)

```bash
curl -X POST "https://jo4-api.jo4.io/api/v1/public/url" \
  -H "Content-Type: application/json" \
  -d '{"longUrl": "https://example.com"}'
```

Limited features, no analytics access.

### Get URL Details

```bash
curl -X GET "https://jo4-api.jo4.io/api/v1/protected/url/{slug}" \
  -H "X-API-Key: $JO4_API_KEY"
```

### Get URL Analytics

```bash
curl -X GET "https://jo4-api.jo4.io/api/v1/protected/url/{slug}/stats" \
  -H "X-API-Key: $JO4_API_KEY"
```

**Response includes:**
- Total clicks
- Clicks by date
- Geographic distribution
- Device/browser breakdown
- Referrer sources

### List My URLs

```bash
curl -X GET "https://jo4-api.jo4.io/api/v1/protected/url/myurls?page=0&size=20" \
  -H "X-API-Key: $JO4_API_KEY"
```

### Update URL

```bash
curl -X PUT "https://jo4-api.jo4.io/api/v1/protected/url/{id}" \
  -H "X-API-Key: $JO4_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Updated Title",
    "longUrl": "https://new-destination.com"
  }'
```

### Delete URL

```bash
curl -X DELETE "https://jo4-api.jo4.io/api/v1/protected/url/{id}" \
  -H "X-API-Key: $JO4_API_KEY"
```

## QR Codes

Every short URL automatically gets a QR code at:
```
https://jo4.io/qr/{shortUrl}
```

## Rate Limits

Rate limits vary by plan:
- Free: 60 requests/minute
- Pro: Up to 10,000 requests/minute
- Anonymous (public endpoints): 10 requests/minute

## API Documentation

Full OpenAPI/Swagger documentation: https://jo4-api.jo4.io/swagger-ui/index.html

## Common Use Cases

### 1. Shorten a URL for sharing
```bash
curl -X POST "https://jo4-api.jo4.io/api/v1/protected/url" \
  -H "X-API-Key: $JO4_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{"longUrl": "https://example.com/article", "title": "Article"}'
```

### 2. Create campaign tracking link
```bash
curl -X POST "https://jo4-api.jo4.io/api/v1/protected/url" \
  -H "X-API-Key: $JO4_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "longUrl": "https://mysite.com/landing",
    "title": "Q1 Campaign",
    "utmSource": "twitter",
    "utmMedium": "social",
    "utmCampaign": "q1-2026"
  }'
```

### 3. Create expiring link
```bash
curl -X POST "https://jo4-api.jo4.io/api/v1/protected/url" \
  -H "X-API-Key: $JO4_API_KEY" \
  -H "Content-Type: application/json" \
  -d '{
    "longUrl": "https://mysite.com/promo",
    "title": "Limited Offer",
    "expirationTime": 1738454400
  }'
```

## Error Codes

| Code | Meaning |
|------|---------|
| 400 | Bad request - invalid parameters |
| 401 | Unauthorized - missing or invalid API key |
| 403 | Forbidden - insufficient permissions |
| 404 | Not found - URL doesn't exist |
| 429 | Rate limit exceeded |

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
