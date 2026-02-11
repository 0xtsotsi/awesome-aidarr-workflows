



# Exa Search

Use Exa’s Search API via the bundled script.

## Requirements

- Set `EXA_API_KEY` in the Gateway environment (recommended) or in `~/.openclaw/.env`.

## Commands

- Run a search:
  - `node {baseDir}/scripts/exa_search.mjs "<query>" --count 5`

- Include page text in results (costs more):
  - `node {baseDir}/scripts/exa_search.mjs "<query>" --count 5 --text`

- Narrow by time window:
  - `--start 2025-01-01 --end 2026-02-04`

## Notes

- This skill does not modify `web_search`; it provides an Exa-backed alternative you can invoke when you specifically want Exa.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
