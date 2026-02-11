# winamp

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/jage9/winamp/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/jage9/winamp/SKILL.md)
> Category: Web & Frontend Development

---

## Description

Control Winamp on Windows (Native or WSL2) or Linux (via Wine).

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Control Winamp on Windows (Native or WSL2) or Linux (via Wine).

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run winamp`)
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
You are executing the winamp workflow. Use the following context:

Description: Control Winamp on Windows (Native or WSL2) or Linux (via Wine).

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: winamp
category: Web & Frontend Development
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Winamp CLI

Use this skill to control the Winamp media player.

## Executable Paths
Depending on your environment, the path to the Winamp executable will vary:
- **Windows (Native):** `C:\Program Files (x86)\Winamp\winamp.exe`
- **WSL2 (Windows Host):** `/mnt/c/Program Files (x86)/Winamp/winamp.exe`
- **Linux (via Wine):** `wine "C:\Program Files (x86)\Winamp\winamp.exe"`

## Common Commands

### Playback Control
- **Play:** `winamp.exe /PLAY`
- **Pause/Unpause:** `winamp.exe /PAUSE`
- **Stop:** `winamp.exe /STOP`
- **Next Track:** `winamp.exe /NEXT`
- **Previous Track:** `winamp.exe /PREV`

### Managing Playlists
- **Play File (Clear Queue):** `winamp.exe "C:\path\to\file.mp3"`
- **Enqueue File/Folder:** `winamp.exe /ADD "C:\path\to\file.mp3"`
- **Play Playlist:** `winamp.exe "C:\path\to\playlist.m3u"`

### Advanced Switches
- **New Instance:** `winamp.exe /NEW` (Forces a new window)
- **Specific Instance:** `winamp.exe /CLASS="MyClassName"` (Target a specific window)
- **Config Dir:** `winamp.exe /INIDIR="C:\path\to\dir"` (Use specific settings)

## Execution Note (Backgrounding)
Since Winamp is a GUI application, always run it in the background to prevent sessions from hanging. The command will execute as soon as it is sent.

### Moltbot `exec` Usage:
Set `background: true` in your tool call.

```json
{
  "tool": "exec",
  "command": "\"/mnt/c/Program Files (x86)/Winamp/winamp.exe\" \"C:\\path\\to\\file.mp3\"",
  "background": true
}
```

### CLI Usage:
Append an ampersand (`&`) to the command.
```bash
"/mnt/c/Program Files (x86)/Winamp/winamp.exe" /PLAY &
```


---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
