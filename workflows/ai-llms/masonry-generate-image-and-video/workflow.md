# masonry-generate-image-and-video

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/junaid1460/masonry-generate-image-and-video/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/junaid1460/masonry-generate-image-and-video/SKILL.md)
> Category: AI & LLMs

---

## Description

AI-powered image and video generation using the Masonry CLI. Generate images, videos, check job status, and manage media assets.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
AI-powered image and video generation using the Masonry CLI. Generate images, videos, check job status, and manage media assets.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run masonry-generate-image-and-video`)
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
You are executing the masonry-generate-image-and-video workflow. Use the following context:

Description: AI-powered image and video generation using the Masonry CLI. Generate images, videos, check job status, and manage media assets.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: masonry-generate-image-and-video
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Masonry CLI

The `masonry` CLI provides AI-powered image and video generation capabilities.

## When to use this skill

Use this skill when the user wants to:
- Generate images from text prompts
- Generate videos from text prompts
- Check status of generation jobs
- Download generated media
- List available AI models
- View generation history

## Installation

If the masonry command is not available, install it:

```bash
curl -sSL https://media.masonry.so/cli/install.sh | sh
```

## Quick Commands

```bash
# Generate image
masonry image "your prompt here" --aspect 16:9

# Generate video
masonry video "your prompt here" --duration 4

# Check job status
masonry job status <job-id>

# Download result
masonry job download <job-id> -o ./output.png

# List available models
masonry models list --type image
masonry models list --type video
```

## Detailed Workflows

### Image Generation

```bash
# Basic generation
masonry image "a sunset over mountains, photorealistic"

# With options
masonry image "cyberpunk cityscape" --aspect 16:9 --model imagen-3.0-generate-002

# Available flags
#   --aspect, -a     Aspect ratio (16:9, 9:16, 1:1)
#   --dimension, -d  Exact size (1920x1080)
#   --model, -m      Model key
#   --output, -o     Output path
#   --negative-prompt What to avoid
#   --seed           Reproducibility seed
```

### Video Generation

```bash
# Basic generation
masonry video "ocean waves crashing on rocks"

# With options
masonry video "drone shot of forest" --duration 6 --aspect 16:9

# Available flags
#   --duration       Length in seconds (4, 6, 8)
#   --aspect, -a     Aspect ratio (16:9, 9:16)
#   --model, -m      Model key
#   --image, -i      First frame image
#   --no-audio       Disable audio generation
```

### Job Management

```bash
# List recent jobs
masonry job list

# Check specific job
masonry job status <job-id>

# Wait for completion and download
masonry job wait <job-id> --download -o ./result.png

# View local history
masonry history list
masonry history pending --sync
```

### Model Discovery

```bash
# List all models
masonry models list

# Filter by type
masonry models list --type video

# Get model parameters
masonry models params veo-3.1-fast-generate-preview
```

## Response Format

All commands return JSON:

```json
{
  "success": true,
  "job_id": "abc-123",
  "status": "pending",
  "check_after_seconds": 10,
  "check_command": "masonry job status abc-123"
}
```

## Authentication

If commands fail with auth errors:

```bash
masonry login
```

## Enhanced Project Skills

For project-specific skills with detailed workflows, run:

```bash
masonry skill install
```

This installs additional skills to `.claude/skills/`:
- `masonry-generate` - Detailed generation workflow
- `masonry-models` - Model exploration
- `masonry-jobs` - Job management

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
