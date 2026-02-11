# avatar-video-messages

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/thewulf7/avatar-video-messages/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/thewulf7/avatar-video-messages/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Generate and send video messages with a lip-syncing VRM avatar. Use when user asks for video message, avatar video, video reply, or when TTS should be delivered as video instead of audio.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Generate and send video messages with a lip-syncing VRM avatar. Use when user asks for video message, avatar video, video reply, or when TTS should be delivered as video instead of audio.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run avatar-video-messages`)
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
You are executing the avatar-video-messages workflow. Use the following context:

Description: Generate and send video messages with a lip-syncing VRM avatar. Use when user asks for video message, avatar video, video reply, or when TTS should be delivered as video instead of audio.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: avatar-video-messages
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Video Message

Generate avatar video messages from text or audio. Outputs as Telegram video notes (circular format).

## Installation

```bash
npm install -g openclaw-avatarcam
```

## Configuration

Configure in `TOOLS.md`:

```markdown
### Video Message (avatarcam)
- avatar: default.vrm
- background: #00FF00
```

### Settings Reference

| Setting | Default | Description |
|---------|---------|-------------|
| `avatar` | `default.vrm` | VRM avatar file path |
| `background` | `#00FF00` | Color (hex) or image path |

## Prerequisites

### System Dependencies

| Platform | Command |
|----------|---------|
| **macOS** | `brew install ffmpeg` |
| **Linux** | `sudo apt-get install -y xvfb xauth ffmpeg` |
| **Windows** | Install ffmpeg and add to PATH |
| **Docker** | See Docker section below |

> **Note:** macOS and Windows don't need xvfb — they have native display support.

### Docker Users
Add to `OPENCLAW_DOCKER_APT_PACKAGES`:
```
build-essential procps curl file git ca-certificates xvfb xauth libgbm1 libxss1 libatk1.0-0 libatk-bridge2.0-0 libgdk-pixbuf2.0-0 libgtk-3-0 libasound2 libnss3 ffmpeg
```

## Usage

```bash
# With color background
avatarcam --audio voice.mp3 --output video.mp4 --background "#00FF00"

# With image background
avatarcam --audio voice.mp3 --output video.mp4 --background "./bg.png"

# With custom avatar
avatarcam --audio voice.mp3 --output video.mp4 --avatar "./custom.vrm"
```

## Sending as Video Note

Use OpenClaw's `message` tool with `asVideoNote`:

```
message action=send filePath=/tmp/video.mp4 asVideoNote=true
```

## Workflow

1. **Read config** from TOOLS.md (avatar, background)
2. **Generate TTS** if given text: `tts text="..."` → audio path
3. **Run avatarcam** with audio + settings → MP4 output
4. **Send as video note** via `message action=send filePath=... asVideoNote=true`
5. **Return NO_REPLY** after sending

## Example Flow

User: "Send me a video message saying hello"

```bash
# 1. TTS
tts text="Hello! How are you today?" → /tmp/voice.mp3

# 2. Generate video
avatarcam --audio /tmp/voice.mp3 --output /tmp/video.mp4 --background "#00FF00"

# 3. Send as video note
message action=send filePath=/tmp/video.mp4 asVideoNote=true

# 4. Reply
NO_REPLY
```

## Technical Details

| Setting | Value |
|---------|-------|
| Resolution | 384x384 (square) |
| Frame rate | 30fps constant |
| Max duration | 60 seconds |
| Video codec | H.264 (libx264) |
| Audio codec | AAC |
| Quality | CRF 18 (high quality) |
| Container | MP4 |

### Processing Pipeline
1. Electron renders VRM avatar with lip sync at 1280x720
2. WebM captured via `canvas.captureStream(30)`
3. FFmpeg processes: crop → fps normalize → scale → encode
4. Message tool sends via Telegram `sendVideoNote` API

## Platform Support

| Platform | Display | Notes |
|----------|---------|-------|
| macOS | Native Quartz | No extra deps |
| Linux | xvfb (headless) | `apt install xvfb` |
| Windows | Native | No extra deps |

## Headless Rendering

Avatarcam auto-detects headless environments:
- Uses `xvfb-run` when `$DISPLAY` is not set (Linux only)
- macOS/Windows use native display
- GPU stall warnings are safe to ignore
- Generation time: ~1.5x realtime (20s audio ≈ 30s processing)

## Notes

- Config is read from TOOLS.md
- Clean up temp files after sending: `rm /tmp/video*.mp4`
- For regular video (not circular), omit `asVideoNote=true`

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
