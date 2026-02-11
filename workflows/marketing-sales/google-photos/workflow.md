# google-photos

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jorgermp/google-photos/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jorgermp/google-photos/SKILL.md)
> Category: Marketing & Sales

---

## Description

Manage Google Photos library. Upload photos, create albums, and list library content. Use when the user wants to backup, organize, or share images via Google Photos.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage Google Photos library. Upload photos, create albums, and list library content. Use when the user wants to backup, organize, or share images via Google Photos.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run google-photos`)
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
You are executing the google-photos workflow. Use the following context:

Description: Manage Google Photos library. Upload photos, create albums, and list library content. Use when the user wants to backup, organize, or share images via Google Photos.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: google-photos
category: Marketing & Sales
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Google Photos

This skill provides a way to interact with Google Photos Library API to automate photo management.

## Setup

1. **Enable API**: Enable the "Google Photos Library API" in your Google Cloud Console project.
2. **Credentials**: Download your OAuth 2.0 Client ID credentials as `credentials.json`.
3. **Environment**: This skill uses a Python virtual environment located in its folder.

## Usage

All commands are run through the `scripts/gphotos.py` script.

### List Albums
Useful for finding the ID of an existing album.
```bash
./scripts/gphotos.py --action list --credentials /path/to/credentials.json --token /path/to/token.pickle
```

### Create a New Album
```bash
./scripts/gphotos.py --action create --title "Vacations 2026" --credentials /path/to/credentials.json --token /path/to/token.pickle
```

### Upload a Photo
You can optionally specify an `--album-id` to add the photo to a specific album.
```bash
./scripts/gphotos.py --action upload --photo "/path/to/image.jpg" --album-id "ALBUM_ID" --credentials /path/to/credentials.json --token /path/to/token.pickle
```

## Privacy & Security

- This skill only has access to photos it uploads or that are explicitly shared with the application.
- Credentials and tokens are stored locally and should be kept secure.
- Never share your `credentials.json` or `token.pickle` files.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
