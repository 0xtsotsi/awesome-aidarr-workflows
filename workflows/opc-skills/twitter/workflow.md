# Twitter/X Workflow

**Status:** Active
**Date:** 2026-02-21
**Use Case:** Search and retrieve content from Twitter/X
**Source:** Adapted from OPC Skills (resciencelab/opc-skills)

## Overview

Get user profiles, tweets, replies, followers/following, communities, spaces, and trends from Twitter/X via twitterapi.io.

## ATLAS Alignment

| ATLAS Phase | Workflow Step |
|-------------|---------------|
| Architect | Define search target and scope |
| Trace | Retrieve user/tweet data |
| Link | Connect to twitterapi.io endpoints |
| Assemble | Process and present results |
| Stress-test | Verify data accuracy |

## Trigger

This workflow is invoked when user mentions:
- Twitter, X, tweets
- Search Twitter for content
- Get user info, followers, trends

## Prerequisites

Set API key in `~/.zshrc`:
```bash
export TWITTERAPI_API_KEY="your_api_key"
```

**Quick Test:**
```bash
python3 scripts/get_user_info.py elonmusk
```

## User Endpoints

```bash
python3 scripts/get_user_info.py USERNAME
python3 scripts/get_user_about.py USERNAME
python3 scripts/get_user_tweets.py USERNAME --limit 20
python3 scripts/get_user_mentions.py USERNAME --limit 20
python3 scripts/get_followers.py USERNAME --limit 100
python3 scripts/get_following.py USERNAME --limit 100
python3 scripts/check_relationship.py USER1 USER2
python3 scripts/search_users.py "query" --limit 20
```

## Tweet Endpoints

```bash
python3 scripts/get_tweet.py TWEET_ID
python3 scripts/search_tweets.py "query" --type Latest --limit 20
python3 scripts/get_tweet_replies.py TWEET_ID --limit 20
python3 scripts/get_tweet_quotes.py TWEET_ID --limit 20
python3 scripts/get_tweet_thread.py TWEET_ID
```

## Search Syntax

```bash
# Basic search
python3 scripts/search_tweets.py "AI agent"

# From specific user
python3 scripts/search_tweets.py "from:elonmusk"

# Date range
python3 scripts/search_tweets.py "AI since:2024-01-01 until:2024-12-31"

# Exclude retweets
python3 scripts/search_tweets.py "AI -filter:retweets"

# With media
python3 scripts/search_tweets.py "AI filter:media"

# Minimum engagement
python3 scripts/search_tweets.py "AI min_faves:1000"
```

## Community Endpoints

```bash
python3 scripts/get_community.py COMMUNITY_ID
python3 scripts/get_community_members.py COMMUNITY_ID --limit 20
python3 scripts/get_community_tweets.py COMMUNITY_ID --limit 20
```

## API Reference

- **Base URL:** https://api.twitterapi.io/twitter
- **Auth:** X-API-Key header
- **Pricing:** ~$0.15-0.18/1k requests
- **Docs:** https://docs.twitterapi.io/
