# ytmusic

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/gentrycopsy/ytmusic/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/gentrycopsy/ytmusic/SKILL.md)
> Category: Media & Streaming

---

## Description

Manage YouTube Music library, playlists, and discovery via ytmusicapi.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Manage YouTube Music library, playlists, and discovery via ytmusicapi.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run ytmusic`)
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
You are executing the ytmusic workflow. Use the following context:

Description: Manage YouTube Music library, playlists, and discovery via ytmusicapi.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: ytmusic
category: Media & Streaming
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# YTMusic Librarian

This skill uses the `ytmusicapi` Python library to interact with YouTube Music.

## Prerequisites

- Python 3.x
- `ytmusicapi` package: `pip install ytmusicapi`
- Authentication file (`oauth.json` or `browser.json`) in the skill folder.

## Setup Instructions

1. **Install the library:**
   ```bash
   pip install ytmusicapi
   ```

2. **Generate Authentication (The "cURL Handshake"):**
   - Open **Microsoft Edge** and visit [music.youtube.com](https://music.youtube.com) (ensure you are logged in).
   - Press `F12` to open DevTools, go to the **Network** tab.
   - Click your **Profile Icon -> Library** on the page.
   - Look for a request named `browse` in the network list.
   - **Right-click** the `browse` request -> **Copy -> Copy as cURL (bash)**.
   - Paste that cURL command into a file named `headers.txt` in the skill folder.
   - Run the following Python snippet to generate `browser.json`:
     ```python
     from ytmusicapi.auth.browser import setup_browser
     with open('headers.txt', 'r') as f:
         setup_browser('browser.json', f.read())
     ```
   - Ensure `browser.json` is located in the skill folder.

3. **Verify:**
   ```bash
   python -c "from ytmusicapi import YTMusic; yt = YTMusic('browser.json'); print(yt.get_library_songs(limit=1))"
   ```

## Workflows

### Library Management
- List songs/albums: `yt.get_library_songs()`, `yt.get_library_albums()`
- Add/Remove: `yt.rate_song(videoId, 'LIKE')`, `yt.edit_song_library_status(feedbackToken)`

### Playlist Management
- Create: `yt.create_playlist(title, description)`
- Add Tracks: `yt.add_playlist_items(playlistId, [videoIds])`
- Remove Tracks: `yt.remove_playlist_items(playlistId, [videoIds])`

### Metadata & Discovery
- Get Lyrics: `yt.get_lyrics(browseId)`
- Get Related: `yt.get_watch_playlist(videoId)` -> `related`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
