# xiaohongshu-mcp

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/pxfeng/xiaohongshu-mcp/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/pxfeng/xiaohongshu-mcp/SKILL.md)
> Category: Browser & Automation

---

## Description

Upload images and videos to Xiaohongshu Creator Platform using a local MCP server with browser automation. Features enhanced title validation and improved draft saving.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Upload images and videos to Xiaohongshu Creator Platform using a local MCP server with browser automation. Features enhanced title validation and improved draft saving.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run xiaohongshu-mcp`)
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
You are executing the xiaohongshu-mcp workflow. Use the following context:

Description: Upload images and videos to Xiaohongshu Creator Platform using a local MCP server with browser automation. Features enhanced title validation and improved draft saving.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: xiaohongshu-mcp
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Xiaohongshu Uploader Skill

This skill provides a Model Context Protocol (MCP) server that allows Clawdbot to upload content to Xiaohongshu.

## Features

- **Smart Login**: Automates login session persistence. Just scan the QR code once.
- **Auto-Upload**: Supports uploading images with titles and descriptions via natural language commands.
- **Title Validation**: Automatically validates and trims titles to under 20 characters to ensure proper saving.
- **Enhanced Save Functionality**: Uses "暂存离开" (Save and Exit) button for more reliable draft saving.
- **Browser Automation**: Leveraging Playwright for robust interaction with the Creator Platform.
- **Improved Error Handling**: Better fallback mechanisms and error reporting.

## Prerequisites

- Node.js installed.
- Playwright browsers installed (the setup script will handle this).

## Setup

1.  Navigate to the `server` directory:
    ```bash
    cd server
    npm install
    npm run build
    npx playwright install chromium
    ```

2.  Add to your Clawdbot/Claude Desktop configuration:

    ```json
    {
      "mcpServers": {
        "xiaohongshu": {
          "command": "node",
          "args": [
            "/ABSOLUTE/PATH/TO/xiaohongshu-upload-skill/server/build/index.js"
          ]
        }
      }
    }
    ```
    *Note: Replace `/ABSOLUTE/PATH/TO` with the actual full path to this skill folder.*

## Usage

### 1. Login
First time use requires login.
- **Command**: "Login to Xiaohongshu"
- **Action**: Scan the QR code in the popped-up browser.
- **Confirmation**: Wait for the browser to close or the tool to report success.

### 2. Upload
- **Command**: "Upload [file] to Xiaohongshu with title [title] and description [content]"
- **Action**: The agent will automate the upload process.
- **Automatic Title Validation**: If your title exceeds 20 characters, it will be automatically truncated to ensure proper saving.

## Troubleshooting

- **Login Failed**: Ensure you didn't close the window manually before the success message.
- **Browser not opening**: Check if `npx playwright install` was run.
- **Draft not saving**: Titles must be under 20 characters. The system will automatically truncate longer titles.
- **Save button not found**: The system now tries multiple save button variations including "暂存离开", "保存草稿", and "存草稿".
---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
