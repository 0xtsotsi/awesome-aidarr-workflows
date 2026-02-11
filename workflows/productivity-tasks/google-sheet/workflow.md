# google-sheet

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/longmaba/google-sheet/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/longmaba/google-sheet/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Read, write, append, and manage Google Sheets via the Google Sheets API (Node.js SDK). Use when you need to interact with spreadsheets — reading data, writing/updating cells, appending rows, clearing ranges, formatting cells, managing sheets. Requires a Google Cloud service account with Sheets API enabled.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Read, write, append, and manage Google Sheets via the Google Sheets API (Node.js SDK). Use when you need to interact with spreadsheets — reading data, writing/updating cells, appending rows, clearing ranges, formatting cells, managing sheets. Requires a Google Cloud service account with Sheets API enabled.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run google-sheet`)
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
You are executing the google-sheet workflow. Use the following context:

Description: Read, write, append, and manage Google Sheets via the Google Sheets API (Node.js SDK). Use when you need to interact with spreadsheets — reading data, writing/updating cells, appending rows, clearing ranges, formatting cells, managing sheets. Requires a Google Cloud service account with Sheets API enabled.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: google-sheet
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Google Sheets Skill

Interact with Google Sheets using a service account.

## Setup (One-time)

1. **Google Cloud Console:**
   - Create/select a project
   - Enable "Google Sheets API"
   - Create a Service Account (IAM → Service Accounts → Create)
   - Download JSON key

2. **Configure credentials** (one of these):
   - Set env: `GOOGLE_SERVICE_ACCOUNT_KEY=/path/to/key.json`
   - Place `service-account.json` or `credentials.json` in the skill directory
   - Place in `~/.config/google-sheets/credentials.json`

3. **Share sheets** with the service account email (found in JSON key as `client_email`)

4. **Install dependencies:**
   ```bash
   cd skills/google-sheets && npm install
   ```

## Usage

```bash
node scripts/sheets.js <command> [args]
```

## Commands

### Data Operations

| Command | Args | Description |
|---------|------|-------------|
| `read` | `<id> <range>` | Read cells |
| `write` | `<id> <range> <json>` | Write data |
| `append` | `<id> <range> <json>` | Append rows |
| `clear` | `<id> <range>` | Clear range |

### Formatting

| Command | Args | Description |
|---------|------|-------------|
| `format` | `<id> <range> <formatJson>` | Format cells |
| `getFormat` | `<id> <range>` | Get cell formats |
| `borders` | `<id> <range> [styleJson]` | Add borders |
| `copyFormat` | `<id> <source> <dest>` | Copy format between ranges |
| `merge` | `<id> <range>` | Merge cells |
| `unmerge` | `<id> <range>` | Unmerge cells |

### Layout

| Command | Args | Description |
|---------|------|-------------|
| `resize` | `<id> <sheet> <cols\|rows> <start> <end> <px>` | Resize columns/rows |
| `autoResize` | `<id> <sheet> <startCol> <endCol>` | Auto-fit columns |
| `freeze` | `<id> <sheet> [rows] [cols]` | Freeze rows/columns |

### Sheet Management

| Command | Args | Description |
|---------|------|-------------|
| `create` | `<title>` | Create spreadsheet |
| `info` | `<id>` | Get metadata |
| `addSheet` | `<id> <title>` | Add sheet tab |
| `deleteSheet` | `<id> <sheetName>` | Delete sheet tab |
| `renameSheet` | `<id> <oldName> <newName>` | Rename sheet tab |

## Examples

```bash
# Read data
node scripts/sheets.js read "SPREADSHEET_ID" "Sheet1!A1:C10"

# Write data
node scripts/sheets.js write "SPREADSHEET_ID" "Sheet1!A1:B2" '[["Name","Score"],["Alice",95]]'

# Format cells (yellow bg, bold)
node scripts/sheets.js format "SPREADSHEET_ID" "Sheet1!A1:B2" '{"backgroundColor":{"red":255,"green":255,"blue":0},"textFormat":{"bold":true}}'

# Copy format from one range to another
node scripts/sheets.js copyFormat "SPREADSHEET_ID" "Sheet1!A1:C3" "Sheet1!D1:F3"

# Add borders
node scripts/sheets.js borders "SPREADSHEET_ID" "Sheet1!A1:C3"

# Resize columns to 150px
node scripts/sheets.js resize "SPREADSHEET_ID" "Sheet1" cols A C 150

# Auto-fit column widths
node scripts/sheets.js autoResize "SPREADSHEET_ID" "Sheet1" A Z

# Freeze first row and column
node scripts/sheets.js freeze "SPREADSHEET_ID" "Sheet1" 1 1

# Add new sheet tab
node scripts/sheets.js addSheet "SPREADSHEET_ID" "NewSheet"
```

## Format Options

```json
{
  "backgroundColor": {"red": 255, "green": 255, "blue": 0},
  "textFormat": {
    "bold": true,
    "italic": false,
    "fontSize": 12,
    "foregroundColor": {"red": 0, "green": 0, "blue": 0}
  },
  "horizontalAlignment": "CENTER",
  "verticalAlignment": "MIDDLE",
  "wrapStrategy": "WRAP"
}
```

## Border Style

```json
{
  "style": "SOLID",
  "color": {"red": 0, "green": 0, "blue": 0}
}
```

Border styles: DOTTED, DASHED, SOLID, SOLID_MEDIUM, SOLID_THICK, DOUBLE

## Finding Spreadsheet ID

From URL: `https://docs.google.com/spreadsheets/d/SPREADSHEET_ID/edit`

## Troubleshooting

- **403 Forbidden**: Sheet not shared with service account email
- **404 Not Found**: Wrong spreadsheet ID or sheet name

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
