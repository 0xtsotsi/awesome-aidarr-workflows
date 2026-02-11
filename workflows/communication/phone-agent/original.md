



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
