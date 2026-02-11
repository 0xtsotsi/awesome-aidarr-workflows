# tubeclaw

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/snail3d/tubeclaw/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/snail3d/tubeclaw/SKILL.md)
> Category: Media & Streaming

---

## Description

No description available.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
What this workflow accomplishes.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run tubeclaw`)
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
You are executing the tubeclaw workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: tubeclaw
category: Media & Streaming
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# TubeClaw - YouTube Video Analyzer

Analyze any YouTube video, extract key insights, remove fluff, and provide actionable summaries with relevant links.

## What It Does

- 📥 Fetches YouTube video transcripts
- 🧠 Analyzes content for key insights
- ✂️ Removes advertising/sponsorship fluff
- 🔗 Extracts mentioned resources/tools/links
- 📝 Provides clean, actionable summary

## Usage

### Command Line
```bash
node analyze.js --url "https://youtube.com/watch?v=..."
```

### Programmatic
```javascript
const { analyzeVideo } = require('./analyze');

const result = await analyzeVideo('https://youtube.com/watch?v=...');
console.log(result.summary);
console.log(result.keyPoints);
console.log(result.resources);
```

## Requirements

- Node.js 14+
- OpenClaw/Clawdbot with youtube-transcript skill
- AI model access (Claude/OpenAI) for analysis

## How It Works

1. **Extract Transcript** - Uses video-transcript-downloader skill
2. **Clean Content** - Removes ads, sponsorships, filler words
3. **Analyze** - AI extracts key insights and topics
4. **Find Resources** - Identifies mentioned tools, links, GitHub repos
5. **Summarize** - Generates actionable summary

## Example Output

```json
{
  "title": "Video Title",
  "channel": "Channel Name",
  "summary": "Clean summary without fluff...",
  "keyPoints": [
    "Main insight 1",
    "Main insight 2"
  ],
  "resources": [
    {
      "name": "Tool Name",
      "url": "https://...",
      "context": "Why it's mentioned"
    }
  ],
  "topics": ["AI", "Coding", "Tools"]
}
```

## License

MIT - OpenClaw

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
