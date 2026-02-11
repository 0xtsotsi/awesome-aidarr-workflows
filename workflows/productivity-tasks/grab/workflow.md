# grab

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jamesalmeida/grab/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jamesalmeida/grab/SKILL.md)
> Category: Productivity & Tasks

---

## Description

Download and archive content from URLs (tweets, X articles, Reddit, YouTube). Saves media, text, transcripts, and AI summaries into organized folders.

**Homepage:** https://github.com/jamesalmeida/grab
**Repository:** N/A
**Version:** N/A

**Tags:** download, media, twitter, youtube, reddit, transcript, archive

---

## GOTCHA Framework

### G - Goals
Download and archive content from URLs (tweets, X articles, Reddit, YouTube). Saves media, text, transcripts, and AI summaries into organized folders.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run grab`)
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
You are executing the grab workflow. Use the following context:

Description: Download and archive content from URLs (tweets, X articles, Reddit, YouTube). Saves media, text, transcripts, and AI summaries into organized folders.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: grab
category: Productivity & Tasks
version: 1.0.0
user_invocable: True
homepage: https://github.com/jamesalmeida/grab
```

---

## Original Skill Content



# grab 🫳

Download and archive content from URLs into organized folders.

## Setup

### Dependencies
```bash
brew install yt-dlp ffmpeg openai-whisper
```

### Save Location
On first run, `grab` asks where to save files (default: `~/Dropbox/ClawdBox/`).
Config stored in `~/.config/grab/config`. Reconfigure anytime with `grab --config`.

### Transcription (Local Whisper)
Transcription runs locally via Whisper (`turbo` model) — no API key or network calls needed.

### AI Summaries & Smart Titles (Optional)
Set `OPENAI_API_KEY` to enable:
- AI-generated summaries of content
- Smart descriptive folder names (from transcript/image analysis)

Without it, everything still works — you just won't get summaries or auto-renamed folders.

## What It Does

### Tweets (x.com / twitter.com)
- `tweet.txt` — tweet text, author, date, engagement stats
- `video.mp4` — attached video (if any)
- `image_01.jpg`, etc. — attached images (if any)
- `transcript.txt` — auto-transcribed from video (if video)
- `summary.txt` — AI summary of video (if video)
- Folder named by content description

### X Articles
- `article.txt` — full article text with title, author, date
- `summary.txt` — AI summary of article
- Agent handles via OpenClaw browser snapshot
- Script exits with code 2 and `ARTICLE_DETECTED:<id>:<url>` when it detects an article

### Reddit
- `post.txt` — title, author, subreddit, score, date, body text
- `comments.txt` — top comments with authors and scores
- `image_01.jpg`, etc. — attached images or gallery (if any)
- `video.mp4` — attached video (if any)
- `transcript.txt` — auto-transcribed from video (if video)
- `summary.txt` — AI summary of post + discussion
- If Reddit JSON API is blocked (exit code 3), agent uses OpenClaw browser

### YouTube
- `video.mp4` — the video
- `description.txt` — video description
- `thumbnail.jpg` — video thumbnail
- `transcript.txt` — transcribed audio
- `summary.txt` — AI summary

## Output

Downloads are organized by type:
```
<save_dir>/
  XPosts/
    2026-02-03_embrace-change-you-can-shape-your-life/
      tweet.txt, video.mp4, transcript.txt, summary.txt
  XArticles/
    2026-01-20_the-arctic-smokescreen/
      article.txt, summary.txt
  Youtube/
    2026-02-03_how-to-build-an-ai-agent/
      video.mp4, description.txt, thumbnail.jpg, transcript.txt, summary.txt
  Reddit/
    2026-02-03_maybe-maybe-maybe/
      post.txt, comments.txt, video.mp4, summary.txt
```

## Usage

```bash
grab <url>              # Download and archive a URL
grab --config           # Reconfigure save directory
grab --help             # Show help
```

## Requirements

```bash
brew install yt-dlp ffmpeg openai-whisper
```

Transcription uses local Whisper — no API key needed.
`OPENAI_API_KEY` env var optional — enables AI summaries and smart folder titles.
Without it, media downloads and transcription still work.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
