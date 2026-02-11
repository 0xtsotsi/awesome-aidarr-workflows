# satellite-copilot

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/davestarling/satellite-copilot/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/davestarling/satellite-copilot/SKILL.md)
> Category: Coding Agents & IDEs

---

## Description

Predict satellite passes (NOAA APT, METEOR LRPT, ISS) for a configured latitude/longitude and send WhatsApp alerts with manual dish alignment info (AOS/LOS azimuth+elevation, track direction, inclination). Use when setting up or operating a zero-AI pass scheduler/orchestrator for SDR satellite reception, including configuring NORAD IDs, minimum elevation, alert lead time, and optional remote capture/decode hooks (Pi RTL-SDR capture + Jetson SatDump decode).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Predict satellite passes (NOAA APT, METEOR LRPT, ISS) for a configured latitude/longitude and send WhatsApp alerts with manual dish alignment info (AOS/LOS azimuth+elevation, track direction, inclination). Use when setting up or operating a zero-AI pass scheduler/orchestrator for SDR satellite reception, including configuring NORAD IDs, minimum elevation, alert lead time, and optional remote capture/decode hooks (Pi RTL-SDR capture + Jetson SatDump decode).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run satellite-copilot`)
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
You are executing the satellite-copilot workflow. Use the following context:

Description: Predict satellite passes (NOAA APT, METEOR LRPT, ISS) for a configured latitude/longitude and send WhatsApp alerts with manual dish alignment info (AOS/LOS azimuth+elevation, track direction, inclination). Use when setting up or operating a zero-AI pass scheduler/orchestrator for SDR satellite reception, including configuring NORAD IDs, minimum elevation, alert lead time, and optional remote capture/decode hooks (Pi RTL-SDR capture + Jetson SatDump decode).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: satellite-copilot
category: Coding Agents & IDEs
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# radio-copilot

Plan and alert on satellite passes for SDR reception.

## Quick start

1) Copy the example config:

```bash
mkdir -p ~/.clawdbot/radio-copilot
cp config.example.json ~/.clawdbot/radio-copilot/config.json
chmod 600 ~/.clawdbot/radio-copilot/config.json
```

2) Run the orchestrator once:

```bash
python3 scripts/orchestrator.py
```

3) Run periodically (system cron):

```bash
*/5 * * * * /usr/bin/python3 /path/to/radio-copilot/scripts/orchestrator.py >> ~/.clawdbot/radio-copilot/orchestrator.log 2>&1
```

## What it sends

Alerts include:
- pass start/max/end timestamps
- **AOS** (start) azimuth/elevation
- **LOS** (end) azimuth/elevation
- track direction (AOS→LOS compass)
- orbit inclination

## Notes

- Runtime is **zero-AI** by default.
- Capture/decode hooks are included but disabled until you configure your Pi/Jetson commands.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
