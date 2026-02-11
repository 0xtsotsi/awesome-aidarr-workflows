



# Perplexity Search

AI-powered web search that returns grounded answers with citations.

## Search

Single query:
```bash
node {baseDir}/scripts/search.mjs "what's happening in AI today"
```

Multiple queries (batch):
```bash
node {baseDir}/scripts/search.mjs "What is Perplexity?" "Latest AI news" "Best coffee in NYC"
```

## Options

- `--json`: Output raw JSON response

## Notes

- Requires `PERPLEXITY_API_KEY` environment variable
- Responses include citations when available
- Batch queries are processed in a single API call

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
