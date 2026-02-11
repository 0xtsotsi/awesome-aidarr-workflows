# wooclaw-lite

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/magnum-opus-v1/wooclaw-lite/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/magnum-opus-v1/wooclaw-lite/SKILL.md)
> Category: Clawdbot Tools

---

## Description

Connects to a WooCommerce store via the OpenClaw Connector Lite plugin to fetch orders and products.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Connects to a WooCommerce store via the OpenClaw Connector Lite plugin to fetch orders and products.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run wooclaw-lite`)
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
You are executing the wooclaw-lite workflow. Use the following context:

Description: Connects to a WooCommerce store via the OpenClaw Connector Lite plugin to fetch orders and products.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: wooclaw-lite
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# OpenClaw Connector

This skill allows you to interact with a WooCommerce store. You can check order status, search for products, and verify the store's connection health.

## Configuration

The following environment variables are required:
*   `OPENCLAW_STORE_URL`: The full URL of your WordPress site (e.g., https://example.com).
*   `OPENCLAW_STORE_SECRET`: The Secret Key from the OpenClaw Connector Lite plugin settings.

## Tools

### `check_order`
Use this tool to retrieve detailed information about a specific order.
*   **Input:** `id` (integer) - The Order ID.
*   **Output:** Formatted string with Status, Total, Customer, and Items.

### `find_product`
Use this tool to search for products by name or SKU.
*   **Input:** `query` (string) - The search term.
*   **Output:** List of matching products with IDs, Stock, and Price.

### `store_status`
Use this tool to check if the store is reachable and the plugin is active.
*   **Input:** (None)
*   **Output:** Connection status message.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
