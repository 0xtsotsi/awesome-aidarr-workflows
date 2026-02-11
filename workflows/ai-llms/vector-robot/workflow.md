# vector-robot

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/bogorman/vector-robot/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/bogorman/vector-robot/SKILL.md)
> Category: AI & LLMs

---

## Description

Control Anki Vector robot via wire-pod. Speak through Vector, see through its camera, move head/lift/wheels, change eye colors, trigger animations. Use when user mentions Vector robot, wants to speak through a robot, control a physical robot, or interact with wire-pod.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Control Anki Vector robot via wire-pod. Speak through Vector, see through its camera, move head/lift/wheels, change eye colors, trigger animations. Use when user mentions Vector robot, wants to speak through a robot, control a physical robot, or interact with wire-pod.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run vector-robot`)
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
You are executing the vector-robot workflow. Use the following context:

Description: Control Anki Vector robot via wire-pod. Speak through Vector, see through its camera, move head/lift/wheels, change eye colors, trigger animations. Use when user mentions Vector robot, wants to speak through a robot, control a physical robot, or interact with wire-pod.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: vector-robot
category: AI & LLMs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Vector Robot Control

Control an Anki Vector robot running wire-pod.

## Prerequisites

- Anki Vector robot with escape pod firmware
- wire-pod running (https://github.com/kercre123/wire-pod)
- OpenClaw proxy server for voice input (optional)

## Quick Reference

All API calls require `&serial=SERIAL` parameter. Default: `00501a68`.

```bash
SERIAL="00501a68"
WIREPOD="http://127.0.0.1:8080"
```

### Speech Output

```bash
# Make Vector speak (URL encode the text)
curl -s -X POST "$WIREPOD/api-sdk/assume_behavior_control?priority=high&serial=$SERIAL"
curl -s -X POST "$WIREPOD/api-sdk/say_text?text=Hello%20world&serial=$SERIAL"
curl -s -X POST "$WIREPOD/api-sdk/release_behavior_control?serial=$SERIAL"
```

Or use the helper script: `scripts/vector-say.sh "Hello world"`

### Camera

```bash
# Capture frame from MJPEG stream
timeout 2 curl -s "$WIREPOD/cam-stream?serial=$SERIAL" > /tmp/stream.mjpeg
# Extract JPEG with Python (see scripts/vector-see.sh)
```

### Movement

**⚠️ SAFETY: Cliff sensors are DISABLED during behavior control. Be careful with wheel movements!**

```bash
# Head: speed -2 to 2
curl -s -X POST "$WIREPOD/api-sdk/move_head?speed=2&serial=$SERIAL"  # up
curl -s -X POST "$WIREPOD/api-sdk/move_head?speed=-2&serial=$SERIAL" # down
curl -s -X POST "$WIREPOD/api-sdk/move_head?speed=0&serial=$SERIAL"  # stop

# Lift: speed -2 to 2  
curl -s -X POST "$WIREPOD/api-sdk/move_lift?speed=2&serial=$SERIAL"  # up
curl -s -X POST "$WIREPOD/api-sdk/move_lift?speed=-2&serial=$SERIAL" # down

# Wheels: lw/rw -200 to 200 (USE WITH CAUTION)
curl -s -X POST "$WIREPOD/api-sdk/move_wheels?lw=100&rw=100&serial=$SERIAL"  # forward
curl -s -X POST "$WIREPOD/api-sdk/move_wheels?lw=-50&rw=50&serial=$SERIAL"   # turn left
curl -s -X POST "$WIREPOD/api-sdk/move_wheels?lw=0&rw=0&serial=$SERIAL"      # stop
```

### Settings

```bash
# Volume: 0-5
curl -s -X POST "$WIREPOD/api-sdk/volume?volume=5&serial=$SERIAL"

# Eye color: 0-6
curl -s -X POST "$WIREPOD/api-sdk/eye_color?color=4&serial=$SERIAL"

# Battery status
curl -s "$WIREPOD/api-sdk/get_battery?serial=$SERIAL"
```

### Actions/Intents

```bash
curl -s -X POST "$WIREPOD/api-sdk/cloud_intent?intent=intent_imperative_dance&serial=$SERIAL"
```

Available intents: `intent_imperative_dance`, `intent_system_sleep`, `intent_system_charger`, `intent_imperative_fetchcube`, `explore_start`

## Voice Input (OpenClaw Integration)

To receive voice commands from Vector, run the proxy server:

```bash
node scripts/proxy-server.js
```

Configure wire-pod Knowledge Graph (http://127.0.0.1:8080 → Server Settings):
- Provider: Custom
- API Key: `openclaw`
- Endpoint: `http://localhost:11435/v1`
- Model: `openclaw`

The proxy writes incoming questions to `request.json`. Respond by writing to `response.json`:

```json
{"timestamp": 1234567890000, "answer": "Your response here"}
```

## LaunchAgent (Auto-start on macOS)

Install to `~/Library/LaunchAgents/com.openclaw.vector-proxy.plist` for auto-start. See `scripts/install-launchagent.sh`.

## API Reference

See `references/api.md` for complete endpoint documentation.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
