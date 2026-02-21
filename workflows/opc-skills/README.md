# OPC Workflows

ATLAS/GOTCHA-aligned workflows for AI agents. Adapted from OPC Skills (resciencelab/opc-skills).

## What's Included

| Workflow | Purpose | Trigger Keywords |
|----------|---------|-----------------|
| **seo-geo** | SEO & GEO optimization | SEO, GEO, search visibility, AI ranking |
| **banner-creator** | Create banners via AI | banner, header, hero image |
| **logo-creator** | Create logos via AI | logo, icon, favicon, brand mark |
| **nanobanana** | AI image generation | generate images, create images |
| **twitter** | Twitter/X data retrieval | Twitter, X, tweets |
| **reddit** | Reddit data retrieval | Reddit, subreddit, r/ |
| **producthunt** | Product Hunt data | Product Hunt, PH, product launches |
| **domain-hunter** | Domain search & purchase | buy domain, domain prices |
| **requesthunt** | User demand research | demand research, feature requests |

## ATLAS Framework

Every workflow follows the ATLAS methodology:

| Phase | Purpose |
|-------|---------|
| **Architect** | Define requirements and scope |
| **Trace** | Extract and gather existing data |
| **Link** | Connect to APIs and services |
| **Assemble** | Process and create output |
| **Stress-test** | Validate and verify results |

## GOTCHA Integration

| Component | Application |
|-----------|-------------|
| **Goal** | What the workflow achieves |
| **Obstacles** | Common blockers |
| **Tactics** | Specific techniques |
| **Constraints** | Limits and requirements |
| **Helpers** | Supporting tools/APIs |
| **Alternatives** | Fallback options |

## Usage

Each workflow has a `workflow.md` file with:
- Trigger conditions
- Prerequisites (API keys, dependencies)
- Step-by-step instructions
- Code examples
- Output templates

## Prerequisites

Most workflows require API keys set in `~/.zshrc`:

```bash
# Image Generation
export GEMINI_API_KEY="your_key"

# Twitter/X
export TWITTERAPI_API_KEY="your_key"

# Product Hunt
export PRODUCTHUNT_ACCESS_TOKEN="your_token"

# RequestHunt
export REQUESTHUNT_API_KEY="your_key"

# Logo Processing
export REMOVE_BG_API_KEY="your_key"
export RECRAFT_API_KEY="your_key"
```

## License

Adapted from OPC Skills (resciencelab/opc-skills) with ATLAS/GOTCHA framework alignment.
