# phone-agent

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/kesslerio/phone-agent/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/kesslerio/phone-agent/SKILL.md)
> Category: Communication

---

## Description

Run a real-time AI phone agent using Twilio, Deepgram, and ElevenLabs. Handles incoming calls, transcribes audio, generates responses via LLM, and speaks back via streaming TTS. Use when user wants to: (1) Test voice AI capabilities, (2) Handle phone calls programmatically, (3) Build a conversational voice bot.

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Run a real-time AI phone agent using Twilio, Deepgram, and ElevenLabs. Handles incoming calls, transcribes audio, generates responses via LLM, and speaks back via streaming TTS. Use when user wants to: (1) Test voice AI capabilities, (2) Handle phone calls programmatically, (3) Build a conversational voice bot.

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run phone-agent`)
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
You are executing the phone-agent workflow. Use the following context:

Description: Run a real-time AI phone agent using Twilio, Deepgram, and ElevenLabs. Handles incoming calls, transcribes audio, generates responses via LLM, and speaks back via streaming TTS. Use when user wants to: (1) Test voice AI capabilities, (2) Handle phone calls programmatically, (3) Build a conversational voice bot.

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: phone-agent
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Phone Agent Skill

Runs a local FastAPI server that acts as a real-time voice bridge.

## Architecture

```
Twilio (Phone) <--> WebSocket (Audio) <--> [Local Server] <--> Deepgram (STT)
                                                  |
                                                  +--> OpenAI (LLM)
                                                  +--> ElevenLabs (TTS)
```

## Prerequisites

1.  **Twilio Account**: Phone number + TwiML App.
2.  **Deepgram API Key**: For fast speech-to-text.
3.  **OpenAI API Key**: For the conversation logic.
4.  **ElevenLabs API Key**: For realistic text-to-speech.
5.  **Ngrok** (or similar): To expose your local port 8080 to Twilio.

## Setup

1.  **Install Dependencies**:
    ```bash
    pip install -r scripts/requirements.txt
    ```

2.  **Set Environment Variables** (in `~/.moltbot/.env`, `~/.clawdbot/.env`, or export):
    ```bash
    export DEEPGRAM_API_KEY="your_key"
    export OPENAI_API_KEY="your_key"
    export ELEVENLABS_API_KEY="your_key"
    export TWILIO_ACCOUNT_SID="your_sid"
    export TWILIO_AUTH_TOKEN="your_token"
    export PORT=8080
    ```

3.  **Start the Server**:
    ```bash
    python3 scripts/server.py
    ```

4.  **Expose to Internet**:
    ```bash
    ngrok http 8080
    ```

5.  **Configure Twilio**:
    - Go to your Phone Number settings.
    - Set "Voice & Fax" -> "A Call Comes In" to **Webhook**.
    - URL: `https://<your-ngrok-url>.ngrok.io/incoming`
    - Method: `POST`

## Usage

Call your Twilio number. The agent should answer, transcribe your speech, think, and reply in a natural voice.

## Customization

- **System Prompt**: Edit `SYSTEM_PROMPT` in `scripts/server.py` to change the persona.
- **Voice**: Change `ELEVENLABS_VOICE_ID` to use different voices.
- **Model**: Switch `gpt-4o-mini` to `gpt-4` for smarter (but slower) responses.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
