# snapmaker

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/lucakaufmann/snapmaker/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/lucakaufmann/snapmaker/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Monitor and control Snapmaker 3D printers (U1 with Moonraker/Klipper). Use when checking print status, temperatures, progress, or controlling prints (pause/resume/cancel). Triggers on "printer", "3D print", "Snapmaker", "print status", "nozzle temp", "bed temp".

**Homepage:** N/A
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Monitor and control Snapmaker 3D printers (U1 with Moonraker/Klipper). Use when checking print status, temperatures, progress, or controlling prints (pause/resume/cancel). Triggers on "printer", "3D print", "Snapmaker", "print status", "nozzle temp", "bed temp".

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run snapmaker`)
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
You are executing the snapmaker workflow. Use the following context:

Description: Monitor and control Snapmaker 3D printers (U1 with Moonraker/Klipper). Use when checking print status, temperatures, progress, or controlling prints (pause/resume/cancel). Triggers on "printer", "3D print", "Snapmaker", "print status", "nozzle temp", "bed temp".

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: snapmaker
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Snapmaker Printer Control

Control Snapmaker U1 printers via the Moonraker API.

## Configuration

Create a config file at `~/clawd/config/snapmaker.json`:
```json
{
  "ip": "192.168.x.x",
  "port": 80
}
```

Or use environment variables:
```bash
export SNAPMAKER_IP=192.168.x.x
export SNAPMAKER_PORT=80  # optional, defaults to 80
```

**Config search order:**
1. `SNAPMAKER_IP` environment variable (highest priority)
2. `~/clawd/config/snapmaker.json`
3. `~/.config/clawdbot/snapmaker.json`

## Quick Commands

### Check Status
```bash
scripts/snapmaker.py status
```

### Filament Info
```bash
scripts/snapmaker.py filament
```
Shows RFID tag data for each slot: material type, color (hex), temp ranges, and sensor status.

### Monitor Print (Live)
```bash
scripts/snapmaker.py monitor
```

### Print Control
```bash
scripts/snapmaker.py pause
scripts/snapmaker.py resume  
scripts/snapmaker.py cancel
```

### Temperature
```bash
scripts/snapmaker.py temps
```

## API Reference

The U1 uses Moonraker REST API on port 80:

| Endpoint | Description |
|----------|-------------|
| `/server/info` | Server status |
| `/printer/info` | Printer info |
| `/printer/objects/query?heater_bed&extruder&print_stats` | Status |
| `/printer/print/pause` | Pause print |
| `/printer/print/resume` | Resume print |
| `/printer/print/cancel` | Cancel print |

## Status Response Fields

- `print_stats.state`: `standby`, `printing`, `paused`, `complete`, `error`
- `print_stats.filename`: Current file
- `print_stats.print_duration`: Seconds elapsed
- `virtual_sdcard.progress`: 0.0 to 1.0
- `heater_bed.temperature` / `heater_bed.target`: Bed temps
- `extruder.temperature` / `extruder.target`: Nozzle temps

## Filament & Sensor Data

Query filament RFID and sensors:
```
/printer/objects/query?filament_detect&filament_motion_sensor%20e0_filament&filament_motion_sensor%20e1_filament&filament_motion_sensor%20e2_filament&filament_motion_sensor%20e3_filament
```

### filament_detect.info[]

Array of 4 slots with RFID tag data (or defaults if no tag):

| Field | Description |
|-------|-------------|
| `VENDOR` | "Snapmaker" or "NONE" if no RFID |
| `MANUFACTURER` | e.g. "Polymaker" |
| `MAIN_TYPE` | Material: "PLA", "PETG", "ABS", etc. |
| `SUB_TYPE` | Variant: "SnapSpeed", "generic", etc. |
| `RGB_1` | Color as decimal int (convert: `#${(rgb>>16&0xFF).toString(16)}...`) |
| `ARGB_COLOR` | Color with alpha (decimal) |
| `WEIGHT` | Spool weight in grams |
| `HOTEND_MIN_TEMP` / `HOTEND_MAX_TEMP` | Nozzle temp range |
| `BED_TEMP` | Recommended bed temp |
| `OFFICIAL` | true if official Snapmaker filament |

### filament_motion_sensor e{0-3}_filament

| Field | Description |
|-------|-------------|
| `filament_detected` | Boolean - filament present in slot |
| `enabled` | Boolean - sensor active |

**Note:** Slots can have `filament_detected: true` but `VENDOR: NONE` — this means third-party filament without RFID tag.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
