# switchbot

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/daaab/switchbot/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/daaab/switchbot/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Control SwitchBot smart home devices (curtains, plugs, lights, locks, etc.) via SwitchBot Cloud API. Use when user asks to open/close curtains, turn on/off lights/plugs, check temperature/humidity, or control any SwitchBot device.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Control SwitchBot smart home devices (curtains, plugs, lights, locks, etc.) via SwitchBot Cloud API. Use when user asks to open/close curtains, turn on/off lights/plugs, check temperature/humidity, or control any SwitchBot device.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run switchbot`)
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
You are executing the switchbot workflow. Use the following context:

Description: Control SwitchBot smart home devices (curtains, plugs, lights, locks, etc.) via SwitchBot Cloud API. Use when user asks to open/close curtains, turn on/off lights/plugs, check temperature/humidity, or control any SwitchBot device.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: switchbot
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# SwitchBot Smart Home Control

Control SwitchBot devices through the Cloud API v1.1.

## First-Time Setup

**Guide your human through these steps:**

### 1. Get API Credentials

Ask your human to:
1. Open **SwitchBot App** on their phone
2. Go to **Profile** (bottom right)
3. Tap **Preferences** (or Settings)
4. Find **About** → **Developer Options**
5. Copy **Token** and **Secret Key**

### 2. Store Credentials Securely

```bash
mkdir -p ~/.config/switchbot
chmod 700 ~/.config/switchbot

cat > ~/.config/switchbot/credentials.json << 'EOF'
{
  "token": "YOUR_TOKEN_HERE",
  "secret": "YOUR_SECRET_HERE"
}
EOF
chmod 600 ~/.config/switchbot/credentials.json
```

### 3. Discover Devices

Run the discovery script to find all devices:

```bash
python3 <skill_path>/scripts/switchbot.py list
```

### 4. Update Your TOOLS.md

After discovery, note your device IDs in TOOLS.md for quick reference:

```markdown
## SwitchBot Devices
| Device | ID | Type |
|--------|-----|------|
| Living Room Curtain | ABC123 | Curtain3 |
| Bedroom Light | DEF456 | Plug Mini |
```

## Usage

### List All Devices

```bash
python3 <skill_path>/scripts/switchbot.py list
```

### Curtain Control

```bash
# Open curtain (position 0 = fully open)
python3 <skill_path>/scripts/switchbot.py curtain <device_id> open

# Close curtain (position 100 = fully closed)
python3 <skill_path>/scripts/switchbot.py curtain <device_id> close

# Set specific position (0-100)
python3 <skill_path>/scripts/switchbot.py curtain <device_id> 50
```

### Plug/Light Control

```bash
python3 <skill_path>/scripts/switchbot.py plug <device_id> on
python3 <skill_path>/scripts/switchbot.py plug <device_id> off
```

### Check Sensor Status

```bash
python3 <skill_path>/scripts/switchbot.py status <device_id>
```

### Generic Command

```bash
python3 <skill_path>/scripts/switchbot.py command <device_id> <command> [parameter]
```

## Supported Devices

| Device Type | Commands |
|-------------|----------|
| Curtain / Curtain3 | `open`, `close`, `setPosition` |
| Plug Mini / Plug | `turnOn`, `turnOff`, `toggle` |
| Bot | `press`, `turnOn`, `turnOff` |
| Light / Strip Light | `turnOn`, `turnOff`, `setBrightness`, `setColor` |
| Lock | `lock`, `unlock` |
| Humidifier | `turnOn`, `turnOff`, `setMode` |
| Meter / MeterPlus | (read-only: temperature, humidity) |
| Hub / Hub Mini / Hub 2 | (gateway only) |

## Error Handling

| Status Code | Meaning |
|-------------|---------|
| 100 | Success |
| 151 | Device offline |
| 152 | Command not supported |
| 160 | Unknown command |
| 161 | Invalid parameters |
| 190 | Internal error |

## Tips for Agents

1. **First interaction**: If no credentials exist, guide the human through setup
2. **Device aliases**: Create friendly names in TOOLS.md (e.g., "living room" → device ID)
3. **Batch operations**: Multiple devices can be controlled in sequence
4. **Status checks**: Use `status` command before reporting sensor readings
5. **Error recovery**: If device is offline (151), suggest checking Hub connection

## Security Notes

- Credentials file should be chmod 600
- Never log or display the token/secret
- API calls are made over HTTPS to api.switch-bot.com

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
