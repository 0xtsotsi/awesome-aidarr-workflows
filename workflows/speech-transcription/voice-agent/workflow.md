# voice-agent

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/ricardotrevisan/voice-agent/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/ricardotrevisan/voice-agent/SKILL.md)
> Category: Speech & Transcription

---

## Description

Local Voice Input/Output for Agents using the AI Voice Agent API.

**Homepage:** https://github.com/ricardotrevisan/ai-conversational-skill
**Repository:** N/A
**Version:** 1.0.0

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Local Voice Input/Output for Agents using the AI Voice Agent API.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run voice-agent`)
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
You are executing the voice-agent workflow. Use the following context:

Description: Local Voice Input/Output for Agents using the AI Voice Agent API.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: voice-agent
category: Speech & Transcription
version: 1.0.0
user_invocable: True
homepage: https://github.com/ricardotrevisan/ai-conversational-skill
```

---

## Original Skill Content



# Voice Agent

This skill allows you to speak and listen to the user using the local Voice Agent API.

## Behavior Guidelines
-   **Audio First**: When the user communicates via audio (files), your PRIMARY mode of response is **Audio File**.
-   **Silent Delivery**: When sending an audio response, **DO NOT** send a text explanation like "I sent an audio". Just send the audio file.
-   **Workflow**:
    1.  User sends audio.
    2.  You usage `transcribe` to read it.
    3.  You think of a response.
    4.  You usage `synthesize` to generate the audio file.
    5.  You send the file.
    6.  **STOP**. Do not add text commentary.

## Tools

### Transcribe File
To transcribe an audio file (Speech-to-Text), run the client script with the `transcribe` command.

```bash
python3 {baseDir}/scripts/client.py transcribe "/path/to/audio/file.ogg"
```

### Synthesize to File
To generate audio from text and save it to a file (Text-to-Speech), run the client script with the `synthesize` command.

```bash
python3 {baseDir}/scripts/client.py synthesize "Text to speak" --output "/path/to/output.mp3"
```

### Health Check
To check if the voice agent API is running and healthy:

```bash
python3 {baseDir}/scripts/client.py health
```

### Service Management
If the `Health Check` fails or you receive a connection error, the service may be stopped.
You can attempt to start it by running:

```bash
{baseDir}/scripts/start.sh
```

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
