# phantombuster

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/andrewdmwalker/phantombuster/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/andrewdmwalker/phantombuster/SKILL.md)
> Category: Browser & Automation

---

## Description

Control PhantomBuster automation agents via API. List agents, launch automations, get output/results, check status, and abort running agents. Use when the user needs to run LinkedIn scraping, Twitter automation, lead generation phantoms, or any PhantomBuster workflow.

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Control PhantomBuster automation agents via API. List agents, launch automations, get output/results, check status, and abort running agents. Use when the user needs to run LinkedIn scraping, Twitter automation, lead generation phantoms, or any PhantomBuster workflow.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run phantombuster`)
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
You are executing the phantombuster workflow. Use the following context:

Description: Control PhantomBuster automation agents via API. List agents, launch automations, get output/results, check status, and abort running agents. Use when the user needs to run LinkedIn scraping, Twitter automation, lead generation phantoms, or any PhantomBuster workflow.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: phantombuster
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# PhantomBuster Skill

Control your [PhantomBuster](https://phantombuster.com) automation agents from the command line.

## Setup

1. Get your API key from [Workspace Settings](https://phantombuster.com/workspace-settings)
2. Set the environment variable:
   ```bash
   export PHANTOMBUSTER_API_KEY=your-api-key-here
   ```

## Usage

All commands use the bundled `pb.py` script in this skill's directory.

### List Agents

See all your configured PhantomBuster agents.

```bash
python3 pb.py list
python3 pb.py list --json  # JSON output
```

### Launch an Agent

Start a phantom by ID or name.

```bash
python3 pb.py launch <agent-id>
python3 pb.py launch <agent-id> --argument '{"search": "CEO fintech"}'
```

### Get Agent Output

Fetch the results/output from the most recent run.

```bash
python3 pb.py output <agent-id>
python3 pb.py output <agent-id> --json  # Raw JSON
```

### Check Agent Status

See if an agent is running, finished, or errored.

```bash
python3 pb.py status <agent-id>
```

### Abort Running Agent

Stop an agent that's currently running.

```bash
python3 pb.py abort <agent-id>
```

### Get Agent Details

Full details about a specific agent.

```bash
python3 pb.py get <agent-id>
```

### Fetch Result Data

Download the actual result data (CSV) from an agent's latest run.

```bash
python3 pb.py fetch-result <agent-id>
python3 pb.py fetch-result <agent-id> > output.csv
```

This downloads the `result.csv` file from the agent's S3 storage, perfect for integrating PhantomBuster data into your workflows.

## Example Prompts

- *"List my PhantomBuster agents"*
- *"Launch my LinkedIn Sales Navigator scraper"*
- *"Get the output from agent 12345"*
- *"Check if my Twitter follower phantom is still running"*
- *"Abort the currently running agent"*

## Common Phantoms

PhantomBuster offers many pre-built automations:
- **LinkedIn Sales Navigator Search** — Extract leads from searches
- **LinkedIn Profile Scraper** — Get profile data
- **Twitter Follower Collector** — Scrape followers
- **Instagram Profile Scraper** — Get IG profile data
- **Google Maps Search Export** — Extract business listings

## Rate Limits

PhantomBuster has execution time limits based on your plan. The API itself is not heavily rate-limited, but agent execution consumes your plan's minutes.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
