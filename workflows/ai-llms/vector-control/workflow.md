# vector-control

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/dbeadle1/vector-control/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/dbeadle1/vector-control/SKILL.md)
> Category: AI & LLMs

---

## Description

Control a Vector robot via Wirepod’s local HTTP API on the same network. Use when you need to move Vector, tilt head/lift, speak text, capture camera frames, or run patrol/explore routines from the Pi/Wirepod host. Includes a CLI helper script and endpoint reference.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Control a Vector robot via Wirepod’s local HTTP API on the same network. Use when you need to move Vector, tilt head/lift, speak text, capture camera frames, or run patrol/explore routines from the Pi/Wirepod host. Includes a CLI helper script and endpoint reference.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run vector-control`)
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
You are executing the vector-control workflow. Use the following context:

Description: Control a Vector robot via Wirepod’s local HTTP API on the same network. Use when you need to move Vector, tilt head/lift, speak text, capture camera frames, or run patrol/explore routines from the Pi/Wirepod host. Includes a CLI helper script and endpoint reference.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: vector-control
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Vector Control

## Overview
Control Vector through Wirepod’s `/api-sdk/*` endpoints and the camera stream at `/cam-stream`. Use this skill for movement, speech, camera snapshots, patrols, and exploration from the Pi.

## Quick start (CLI)
Use the bundled script:

```bash
python3 skills/vector-control/scripts/vector_control.py --serial <ESN> assume
python3 skills/vector-control/scripts/vector_control.py --serial <ESN> say --text "Hello Dom"
python3 skills/vector-control/scripts/vector_control.py --serial <ESN> move --lw 160 --rw 160 --time 1.5
python3 skills/vector-control/scripts/vector_control.py --serial <ESN> snapshot --out /tmp/vector.mjpg
```

### Find ESN/serial
If you don’t have it, read:
- `/etc/wire-pod/wire-pod/jdocs/botSdkInfo.json`

## Tasks

### 1) Assume / Release control
Always assume before movement, and release if the bot tips or a human needs manual control.

```bash
python3 .../vector_control.py --serial <ESN> assume
python3 .../vector_control.py --serial <ESN> release
```

### 2) Movement
- `move` sends wheel speeds (0–200 typical). Use short timed moves.

```bash
python3 .../vector_control.py --serial <ESN> move --lw 120 --rw 120 --time 1.0
```

### 3) Head / Lift
```bash
python3 .../vector_control.py --serial <ESN> head --speed -2 --time 1.0
python3 .../vector_control.py --serial <ESN> lift --speed 2 --time 1.0
```

### 4) Speech
Speech can be interrupted by motion/camera. If it fails, pause after speaking before moving.

```bash
python3 .../vector_control.py --serial <ESN> say --text "Sneaking forward"
# wait 1–2s, then move
```

### 5) Camera snapshot
`/cam-stream` returns MJPG. Save it and convert to JPEG if needed (ffmpeg).

```bash
python3 .../vector_control.py --serial <ESN> snapshot --out /tmp/vector.mjpg
ffmpeg -y -loglevel error -i /tmp/vector.mjpg -frames:v 1 /tmp/vector.jpg
```

### 6) Play Audio (MP3/WAV)
Streams an audio file through Vector's speaker. Automatically converts to the required format (8kHz mono WAV).

```bash
python3 .../vector_control.py --serial <ESN> play --file /path/to/music.mp3
```

### 7) Patrol (deterministic sweep)
```bash
python3 .../vector_control.py --serial <ESN> patrol --steps 6 --speed 140 --step-time 1.2 --turn-time 0.8 --speak --phrase "Patrolling"
```

### 8) Explore (randomized wander)
```bash
python3 .../vector_control.py --serial <ESN> explore --steps 8 --speak --phrase "Exploring"
```

## References
- `references/wirepod-api.md` — endpoint list and notes.

## Resources
### scripts/
- `vector_control.py` — CLI for basic control + patrol/explore routines.

### references/
- `wirepod-api.md` — HTTP API endpoints and usage notes.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
