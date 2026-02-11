# skill-exporter

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/macstenk/skill-exporter/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/macstenk/skill-exporter/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Export Clawdbot skills as standalone, deployable microservices. Use when you want to dockerize a skill, deploy it to Railway or Fly.io, or create an independent API service. Generates Dockerfile, FastAPI wrapper, requirements.txt, deployment configs, and optional LLM client integration.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Export Clawdbot skills as standalone, deployable microservices. Use when you want to dockerize a skill, deploy it to Railway or Fly.io, or create an independent API service. Generates Dockerfile, FastAPI wrapper, requirements.txt, deployment configs, and optional LLM client integration.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run skill-exporter`)
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
You are executing the skill-exporter workflow. Use the following context:

Description: Export Clawdbot skills as standalone, deployable microservices. Use when you want to dockerize a skill, deploy it to Railway or Fly.io, or create an independent API service. Generates Dockerfile, FastAPI wrapper, requirements.txt, deployment configs, and optional LLM client integration.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: skill-exporter
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Skill Exporter

Transform Clawdbot skills into standalone, deployable microservices.

## Workflow

```
Clawdbot Skill (tested & working)
         ↓
    skill-exporter
         ↓
Standalone Microservice
         ↓
Railway / Fly.io / Docker
```

## Usage

### Export a skill

```bash
python3 {baseDir}/scripts/export.py \
  --skill ~/.clawdbot/skills/instagram \
  --target railway \
  --llm anthropic \
  --output ~/projects/instagram-service
```

### Options

| Flag | Description | Default |
|------|-------------|---------|
| `--skill` | Path to skill directory | required |
| `--target` | Deployment target: `railway`, `fly`, `docker` | `docker` |
| `--llm` | LLM provider: `anthropic`, `openai`, `none` | `none` |
| `--output` | Output directory | `./<skill-name>-service` |
| `--port` | API port | `8000` |

### Targets

**railway** — Generates `railway.json`, optimized Dockerfile, health checks
**fly** — Generates `fly.toml`, multi-region ready
**docker** — Generic Dockerfile, docker-compose.yml

### LLM Integration

When `--llm` is set, generates `llm_client.py` with:
- Caption/prompt generation
- Decision making helpers
- Rate limiting and error handling

## What Gets Generated

```
<skill>-service/
├── Dockerfile
├── docker-compose.yml
├── api.py              # FastAPI wrapper
├── llm_client.py       # If --llm specified
├── requirements.txt
├── .env.example
├── railway.json        # If --target railway
├── fly.toml            # If --target fly
└── scripts/            # Copied from original skill
    └── *.py
```

## Requirements

The source skill must have:
- `SKILL.md` with valid frontmatter
- At least one script in `scripts/`
- Scripts should be callable (functions, not just inline code)

## Post-Export

1. Copy `.env.example` to `.env` and fill in secrets
2. Test locally: `docker-compose up`
3. Deploy: `railway up` or `fly deploy`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
