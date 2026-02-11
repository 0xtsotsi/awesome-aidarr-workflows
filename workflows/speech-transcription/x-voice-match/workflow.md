# x-voice-match

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/gravyxbt/x-voice-match/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/gravyxbt/x-voice-match/SKILL.md)
> Category: Speech & Transcription

---

## Description

Analyze a Twitter/X account's posting style and generate authentic posts that match their voice. Use when the user wants to create X posts that sound like them, analyze their posting patterns, or maintain consistent voice across posts. Works with Bird CLI integration.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Analyze a Twitter/X account's posting style and generate authentic posts that match their voice. Use when the user wants to create X posts that sound like them, analyze their posting patterns, or maintain consistent voice across posts. Works with Bird CLI integration.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run x-voice-match`)
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
You are executing the x-voice-match workflow. Use the following context:

Description: Analyze a Twitter/X account's posting style and generate authentic posts that match their voice. Use when the user wants to create X posts that sound like them, analyze their posting patterns, or maintain consistent voice across posts. Works with Bird CLI integration.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: x-voice-match
category: Speech & Transcription
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# X Voice Match

Analyze Twitter/X accounts to extract posting patterns and generate authentic content that matches the account owner's unique voice.

## Quick Start

**Step 1: Analyze the account**
```bash
cd /data/workspace/skills/x-voice-match
python3 scripts/analyze_voice.py @username [--tweets 50] [--output profile.json]
```

**Step 2: Generate posts**
```bash
python3 scripts/generate_post.py --profile profile.json --topic "your topic" [--count 3]
```

Or use the all-in-one approach:
```bash
python3 scripts/generate_post.py --account @username --topic "AI agents taking over" --count 5
```

## What It Analyzes

The skill extracts:

- **Length patterns**: Tweet character counts, thread usage, one-liner vs paragraph style
- **Tone markers**: Humor style, sarcasm, self-deprecation, edginess level
- **Topics**: Crypto, AI, tech, memes, personal life, current events
- **Engagement patterns**: QT vs original, reaction tweets, conversation starters
- **Language patterns**: Specific phrases, slang, emoji usage, punctuation style
- **Content types**: Observations, hot takes, memes, threads, questions, personal stories

## Output Format

### Voice Profile (JSON)
```json
{
  "account": "@gravyxbt_",
  "analyzed_tweets": 50,
  "patterns": {
    "avg_length": 85,
    "length_distribution": {"short": 0.6, "medium": 0.3, "long": 0.1},
    "uses_threads": false,
    "humor_style": "self-deprecating, ironic",
    "topics": ["crypto", "AI agents", "memes", "current events"],
    "engagement_type": "reactive QT heavy",
    "signature_phrases": ["lmao", "fr", "based"],
    "emoji_usage": "minimal, strategic",
    "punctuation": "lowercase, casual"
  }
}
```

### Generated Posts
Returns 1-N posts with confidence scores and reasoning.

## Integration with Existing Tools

Works with Bird CLI (`/data/workspace/bird.sh`):
```bash
# Fetch fresh tweets for analysis
./bird.sh user-tweets @gravyxbt_ -n 50 > recent_tweets.txt
python3 scripts/analyze_voice.py --input recent_tweets.txt
```

## Post Type Templates

See [references/post-types.md](references/post-types.md) for common X post frameworks:
- Observations
- Hot takes
- Self-deprecating humor
- Crypto commentary
- Reaction posts
- Questions

## Advanced Usage

### Update Voice Profile
Re-analyze periodically to capture style evolution:
```bash
python3 scripts/analyze_voice.py @username --update profile.json
```

### Generate by Post Type
```bash
python3 scripts/generate_post.py --profile profile.json --type "hot-take" --topic "crypto"
```

### Batch Generation
```bash
python3 scripts/generate_post.py --profile profile.json --batch topics.txt --output posts.json
```

## Workflow

1. **First time**: Run full analysis on 30-50 tweets
2. **Generate posts**: Provide topic, get 3-5 style-matched options
3. **User picks**: Select best option or iterate with feedback
4. **Periodic updates**: Re-analyze monthly or after major voice shifts

## Tips

- **Minimum tweets**: 30 tweets for basic analysis, 50+ for accuracy
- **Recency matters**: Recent tweets reflect current style better than old ones
- **Topic relevance**: Generated posts work best on topics the account normally covers
- **Confidence scores**: <70% = may not sound authentic, revise or regenerate

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
