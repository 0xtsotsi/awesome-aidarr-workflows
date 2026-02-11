# youtube-analytics

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/adamkristopher/youtube-analytics/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/adamkristopher/youtube-analytics/SKILL.md)
> Category: Search & Research

---

## Description

YouTube Data API v3 analytics toolkit. Analyze YouTube channels, videos, and search results. Use when the user asks to: check YouTube channel stats, analyze video performance, compare channels, search for videos, get subscriber counts, view engagement metrics, find trending videos, get channel uploads, or analyze YouTube competition. Requires a YouTube Data API v3 key from Google Cloud Console.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
YouTube Data API v3 analytics toolkit. Analyze YouTube channels, videos, and search results. Use when the user asks to: check YouTube channel stats, analyze video performance, compare channels, search for videos, get subscriber counts, view engagement metrics, find trending videos, get channel uploads, or analyze YouTube competition. Requires a YouTube Data API v3 key from Google Cloud Console.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run youtube-analytics`)
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
You are executing the youtube-analytics workflow. Use the following context:

Description: YouTube Data API v3 analytics toolkit. Analyze YouTube channels, videos, and search results. Use when the user asks to: check YouTube channel stats, analyze video performance, compare channels, search for videos, get subscriber counts, view engagement metrics, find trending videos, get channel uploads, or analyze YouTube competition. Requires a YouTube Data API v3 key from Google Cloud Console.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: youtube-analytics
category: Search & Research
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# YouTube Analytics Toolkit

## Setup

Install dependencies:

```bash
cd scripts && npm install
```

Configure credentials by creating a `.env` file in the project root:

```
YOUTUBE_API_KEY=AIzaSy...your-api-key
YOUTUBE_DEFAULT_MAX_RESULTS=50
```

**Prerequisites**: A Google Cloud project with the YouTube Data API v3 enabled. Get your API key from the [Google Cloud Console](https://console.cloud.google.com/apis/credentials).

## Quick Start

| User says | Function to call |
|-----------|-----------------|
| "Analyze this YouTube channel" | `analyzeChannel(channelId)` |
| "Compare these two channels" | `compareChannels([id1, id2])` |
| "How is this video performing?" | `analyzeVideo(videoId)` |
| "Search YouTube for [topic]" | `searchAndAnalyze(query)` |
| "Get stats for this channel" | `getChannelStats(channelId)` |
| "Get this video's view count" | `getVideoStats(videoId)` |
| "Find channels about [topic]" | `searchChannels(query)` |
| "Show recent uploads from this channel" | `getChannelVideos(channelId)` |

Execute functions by importing from `scripts/src/index.ts`:

```typescript
import { analyzeChannel, searchAndAnalyze } from './scripts/src/index.js';

const analysis = await analyzeChannel('UCxxxxxxxx');
```

Or run directly with tsx:

```bash
npx tsx scripts/src/index.ts
```

## Workflow Pattern

Every analysis follows three phases:

### 1. Analyze
Run API functions. Each call hits the YouTube Data API and returns structured data.

### 2. Auto-Save
All results automatically save as JSON files to `results/{category}/`. File naming patterns:
- Named results: `{sanitized_name}.json`
- Auto-generated: `YYYYMMDD_HHMMSS__{operation}.json`

### 3. Summarize
After analysis, read the saved JSON files and create a markdown summary in `results/summaries/` with data tables, comparisons, and insights.

## High-Level Functions

| Function | Purpose | What it gathers |
|----------|---------|----------------|
| `analyzeChannel(channelId)` | Full channel analysis | Channel info, recent videos, avg views per video |
| `compareChannels(channelIds)` | Compare multiple channels | Side-by-side subscribers, views, video counts |
| `analyzeVideo(videoId)` | Video performance analysis | Views, likes, comments, like rate, comment rate |
| `searchAndAnalyze(query, maxResults?)` | Search + stats | Search results with full video statistics |

## Individual API Functions

For granular control, import specific functions from the API modules. See [references/api-reference.md](references/api-reference.md) for the complete list of 13 API functions with parameters, types, and examples.

### Channel Functions

| Function | Purpose |
|----------|---------|
| `getChannel(channelId)` | Get full channel details |
| `getChannelStats(channelId)` | Get simplified stats (subscribers, views, videoCount) |
| `getMultipleChannels(channelIds)` | Batch fetch multiple channels |

### Video Functions

| Function | Purpose |
|----------|---------|
| `getVideo(videoId)` | Get full video details |
| `getVideoStats(videoId)` | Get simplified stats (views, likes, comments) |
| `getMultipleVideos(videoIds)` | Batch fetch multiple videos |
| `getChannelVideos(channelId)` | Get recent uploads from a channel |

### Search Functions

| Function | Purpose |
|----------|---------|
| `searchVideos(query, options?)` | Search for videos |
| `searchChannels(query, options?)` | Search for channels |

## Results Storage

Results auto-save to `results/` with this structure:

```
results/
├── channels/       # Channel data and comparisons
├── videos/         # Video data and analyses
├── search/         # Search results
└── summaries/      # Human-readable markdown summaries
```

### Managing Results

```typescript
import { listResults, loadResult, getLatestResult } from './scripts/src/index.js';

// List recent results
const files = listResults('channels', 10);

// Load a specific result
const data = loadResult(files[0]);

// Get most recent result for an operation
const latest = getLatestResult('channels', 'channel_analysis');
```

## Tips

1. **Use channel IDs** — Channel IDs start with `UC` (e.g., `UCxxxxxxxx`). You can find them in the channel URL or page source.
2. **Request summaries** — After pulling data, ask for a markdown summary with tables and insights.
3. **Compare channels** — Use `compareChannels()` to benchmark competitors side by side.
4. **Batch requests** — Use `getMultipleChannels()` or `getMultipleVideos()` for efficient batch lookups.
5. **Search + analyze** — `searchAndAnalyze()` combines search with full video stats in one call.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
