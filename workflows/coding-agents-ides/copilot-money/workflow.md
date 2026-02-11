# copilot-money

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jayhickey/copilot-money/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jayhickey/copilot-money/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Query Copilot Money personal finance data (accounts, transactions, net worth, holdings, asset allocation) and refresh bank connections. Use when the user asks about finances, account balances, recent transactions, net worth, investment allocation, or wants to sync/refresh bank data.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Query Copilot Money personal finance data (accounts, transactions, net worth, holdings, asset allocation) and refresh bank connections. Use when the user asks about finances, account balances, recent transactions, net worth, investment allocation, or wants to sync/refresh bank data.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run copilot-money`)
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
You are executing the copilot-money workflow. Use the following context:

Description: Query Copilot Money personal finance data (accounts, transactions, net worth, holdings, asset allocation) and refresh bank connections. Use when the user asks about finances, account balances, recent transactions, net worth, investment allocation, or wants to sync/refresh bank data.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: copilot-money
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Copilot Money CLI

Command-line interface for [Copilot Money](https://copilot.money), a personal finance app. Authenticate once and query accounts, transactions, holdings, and allocation data from your terminal.

> **Note:** This is an unofficial tool and is not affiliated with Copilot Money.

## Install

```bash
pip install copilot-money-cli
```

## Quick start

```bash
copilot-money config init
copilot-money accounts
copilot-money networth
```

## Commands

```bash
copilot-money refresh                     # Refresh all bank connections
copilot-money accounts                    # List accounts with balances
copilot-money accounts --type CREDIT      # Filter by type
copilot-money accounts --json             # Output as JSON
copilot-money transactions                # Recent transactions (default 20)
copilot-money transactions --count 50     # Specify count
copilot-money networth                    # Assets, liabilities, net worth
copilot-money holdings                    # Investment holdings (grouped by type)
copilot-money holdings --group account    # Group by account
copilot-money holdings --group symbol     # Group by symbol
copilot-money holdings --type ETF         # Filter by security type
copilot-money allocation                  # Stocks/bonds with US/Intl split
copilot-money config show                 # Show config and token status
copilot-money config init                 # Auto-detect token from browsers
copilot-money config init --source chrome # From specific browser
copilot-money config init --source manual # Manual token entry
```

## Authentication

Config stored at `~/.config/copilot-money/config.json`. The CLI auto-detects your Copilot Money refresh token from supported browsers on macOS.

- Auto-detect: `copilot-money config init`
- Explicit source: `copilot-money config init --source arc|chrome|safari|firefox`
- Manual entry: `copilot-money config init --source manual`

When using browser auto-detection, the CLI reads your browser's local IndexedDB storage to find your Copilot Money session token. This happens locally — no data is sent anywhere except to Copilot Money's API.

## Requirements

- Python 3.10+
- macOS for browser token extraction (manual token entry works everywhere)

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
