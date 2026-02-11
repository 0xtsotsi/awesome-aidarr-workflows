# loom-workflow

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/g9pedro/loom-workflow/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/g9pedro/loom-workflow/SKILL.md)
> Category: Browser & Automation

---

## Description

AI-native workflow analyzer for Loom recordings. Breaks down recorded business processes
into structured, automatable workflows. Use when:
- Analyzing Loom videos to understand workflows
- Extracting steps, tools, and decision points from screen recordings
- Generating Lobster workflow files from video walkthroughs
- Identifying ambiguities and human intervention points in processes


**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
AI-native workflow analyzer for Loom recordings. Breaks down recorded business processes
into structured, automatable workflows. Use when:
- Analyzing Loom videos to understand workflows
- Extracting steps, tools, and decision points from screen recordings
- Generating Lobster workflow files from video walkthroughs
- Identifying ambiguities and human intervention points in processes


### O - Orchestration
**Trigger:** User-invocable (via `aidarr run loom-workflow`)
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
You are executing the loom-workflow workflow. Use the following context:

Description: AI-native workflow analyzer for Loom recordings. Breaks down recorded business processes
into structured, automatable workflows. Use when:
- Analyzing Loom videos to understand workflows
- Extracting steps, tools, and decision points from screen recordings
- Generating Lobster workflow files from video walkthroughs
- Identifying ambiguities and human intervention points in processes


Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: loom-workflow
category: Browser & Automation
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Loom Workflow Analyzer

Transforms Loom recordings into structured, automatable workflows.

## Quick Start

```bash
# Full pipeline - download, extract, transcribe, analyze
{baseDir}/scripts/loom-workflow analyze https://loom.com/share/abc123

# Individual steps
{baseDir}/scripts/loom-workflow download https://loom.com/share/abc123
{baseDir}/scripts/loom-workflow extract ./video.mp4
{baseDir}/scripts/loom-workflow generate ./analysis.json
```

## Pipeline

1. **Download** - Fetches Loom video via yt-dlp
2. **Smart Extract** - Captures frames at scene changes + transcript timing
3. **Transcribe** - Whisper transcription with word-level timestamps
4. **Analyze** - Multimodal AI analysis (requires vision model)
5. **Generate** - Creates Lobster workflow with approval gates

## Smart Frame Extraction

Frames are captured when:
- **Scene changes** - Significant visual change (ffmpeg scene detection)
- **Speech starts** - New narration segment begins
- **Combined** - Speech + visual change = high-value moment
- **Gap fill** - Max 10s without a frame

## Analysis Output

The analyzer produces:
- `workflow-analysis.json` - Structured workflow definition
- `workflow-summary.md` - Human-readable summary
- `*.lobster` - Executable Lobster workflow file

### Ambiguity Detection

The analyzer flags:
- Unclear mouse movements
- Implicit knowledge ("the usual process")
- Decision points ("depending on...")
- Missing credentials/context
- Tool dependencies

## Vision Analysis Step

After extraction, use the generated prompt with a vision model:

```bash
# The prompt is at: output/workflow-analysis-prompt.md
# Attach frames from: output/frames/

# Example with Claude:
cat output/workflow-analysis-prompt.md | claude --images output/frames/*.jpg
```

Save the JSON response to `workflow-analysis.json`, then:

```bash
{baseDir}/scripts/loom-workflow generate ./output/workflow-analysis.json
```

## Lobster Integration

Generated workflows use:
- `approve` gates for destructive/external actions
- `llm-task` for classification/decision steps
- Resume tokens for interrupted workflows
- JSON piping between steps

## Requirements

- `yt-dlp` - Video download
- `ffmpeg` - Frame extraction + scene detection
- `whisper` - Audio transcription
- Vision-capable LLM for analysis step

## Multilingual Support

Works with any language - Whisper auto-detects and transcribes.
Analysis should be prompted in the video's language for best results.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
