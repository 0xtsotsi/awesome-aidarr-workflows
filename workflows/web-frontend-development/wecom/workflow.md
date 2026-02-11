# wecom

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/qidu/wecom/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/qidu/wecom/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Send messages to WeCom (企业微信) via webhooks using MCP protocol. Works with Claude Code, Claude Desktop, and other MCP clients.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Send messages to WeCom (企业微信) via webhooks using MCP protocol. Works with Claude Code, Claude Desktop, and other MCP clients.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run wecom`)
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
You are executing the wecom workflow. Use the following context:

Description: Send messages to WeCom (企业微信) via webhooks using MCP protocol. Works with Claude Code, Claude Desktop, and other MCP clients.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: wecom
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# WeCom Skill

Send text and markdown messages to WeCom (企业微信) via incoming webhooks.

## Setup

```bash
# Navigate to skill directory
cd skills/wecom

# Install dependencies
npm install

# Build TypeScript
npm run build

# Set webhook URL
export WECOM_WEBHOOK_URL="https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=YOUR_KEY"
```

## Usage with Claude Code

Add to your `~/.config/claude_code/mcp.json`:

```json
{
  "mcpServers": {
    "wecom": {
      "command": "node",
      "args": ["/path/to/clawdbot/skills/wecom/dist/index.js"],
      "env": {
        "WECOM_WEBHOOK_URL": "https://qyapi.weixin.qq.com/cgi-bin/webhook/send?key=YOUR_KEY"
      }
    }
  }
}
```

Then restart Claude Code. You'll have two new tools:

## Tools

### send_wecom_message

Send a text message to WeCom.

```bash
# Simple message
await send_wecom_message({ content: "Hello from Clawdbot!" });

# With mentions
await send_wecom_message({
  content: "Meeting starting now",
  mentioned_list: ["zhangsan", "lisi"]
});
```

### send_wecom_markdown

Send a markdown message (WeCom flavor).

```bash
await send_wecom_markdown({
  content: `# Daily Report
  
**Completed:**
- Task A
- Task B

**Pending:**
- Task C

<@zhangsan>`
});
```

## WeCom Markdown Tags

WeCom supports:

| Feature | Syntax |
|---------|--------|
| Bold | `**text**` or `<strong>text</strong>` |
| Italic | `*text*` or `<i>text</i>` |
| Strikethrough | `~~text~~` or `<s>text</s>` |
| Mention | `<@userid>` |
| Link | `<a href="url">text</a>` |
| Image | `<img src="url" />` |
| Font size | `<font size="5">text</font>` |
| Color | `<font color="#FF0000">text</font>` |

## Environment Variables

| Variable | Required | Default | Description |
|----------|----------|---------|-------------|
| `WECOM_WEBHOOK_URL` | Yes | - | WeCom webhook URL |
| `WECOM_TIMEOUT_MS` | No | 10000 | Request timeout (ms) |

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
