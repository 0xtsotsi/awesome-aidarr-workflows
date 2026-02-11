# jarvis-skills

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/aly-joseph/jarvis-skills/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/aly-joseph/jarvis-skills/SKILL.md)
> Category: Clawdbot Tools

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
**Trigger:** User-invocable (via `aidarr run jarvis-skills`)
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
You are executing the jarvis-skills workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: jarvis-skills
category: Clawdbot Tools
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# Robotic Control Skill (OpenClaw)

## Overview
The Robotic Control skill integrates OpenClaw for physical robotic arm and gripper manipulation through voice commands and programmatic control.

## Slug
robotic-control

## Features
- Robotic arm movement (6-DOF)
- Gripper grab/release operations
- Precise positioning and orientation
- Force/torque sensing
- Collision detection and safety
- Action sequence execution
- Hardware auto-detection
- Simulation mode support

## Implementation
- **Module**: `openclaw_control.py`
- **Primary Library**: `OpenClaw SDK`
- **Communication**: USB Serial, Ethernet, ROS

## Configuration
```python
from openclaw_control import init_claw, get_claw

# Initialize claw
claw = init_claw()

# Control operations
claw.grab(force=50.0)
claw.move_to(10, 20, 30)
claw.release()
```

## Voice Commands
- "Jarvis, grab the object"
- "Jarvis, move to 10 20 30"
- "Jarvis, rotate 45 degrees"
- "Jarvis, release"
- "Jarvis, return to home"
- "Jarvis, claw status"

## Hardware Support
- Universal Robots (UR)
- ABB Robotics
- KUKA
- Stäubli
- Custom embedded systems

## Performance
- Reach: 2-3 meters (model-dependent)
- Payload: 3-500 kg (model-dependent)
- Precision: ±0.03-0.1 mm
- Speed: 1-7000 mm/s
- Response Time: <10ms

## Dependencies
- openclaw
- pyserial
- numpy

## Author
Aly-Joseph

## Version
2.0.0

## Last Updated
2026-01-31

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
