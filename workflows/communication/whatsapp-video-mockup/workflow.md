# whatsapp-video-mockup

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/danpeg/whatsapp-video-mockup/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/danpeg/whatsapp-video-mockup/SKILL.md)
> Category: Communication

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
**Trigger:** User-invocable (via `aidarr run whatsapp-video-mockup`)
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
You are executing the whatsapp-video-mockup workflow. Use the following context:

Description: 

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: whatsapp-video-mockup
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content

# WhatsApp Video Skill

Create animated WhatsApp-style chat videos using Remotion. Perfect for X, TikTok, Instagram Reels.

## Features

- 📱 Realistic iPhone frame with Dynamic Island
- 💬 WhatsApp dark mode UI (accurate colors, bubbles, timestamps)
- 📜 Auto-scrolling as messages extend
- 🔤 Large, readable fonts (optimized for mobile viewing)
- 🎵 Message notification sounds
- ✨ Spring animations on message appearance
- ⌨️ Typing indicator ("..." bubbles)
- 🔗 Link preview cards
- ✅ Read receipts (blue checkmarks)
- **Bold** and `code` formatting support

## Default Settings

- **Aspect ratio:** 4:5 (1080×1350) - optimal for X/Instagram feed
- **No intro/outro** - starts and ends with the chat
- **2x fonts** - readable on mobile devices
- **Auto-scroll** - keeps all messages visible

## Prerequisites

This skill requires the **Remotion Best Practices** skill:

```bash
npx skills add remotion-dev/skills -a claude-code -y -g
```

## Quick Start

```bash
cd ~/Projects/remotion-test
```

Edit the conversation in `src/WhatsAppVideo.tsx`, then render:

```bash
npx remotion render WhatsAppDemo out/my-video.mp4 --concurrency=4
```

## How to Create a New Video

### 1. Define Your Messages

Edit the `ChatMessages` component in `src/WhatsAppVideo.tsx`:

```tsx
// Incoming message (from assistant)
<Message
  text="Your message text here"
  isOutgoing={false}
  time="8:40 AM"
  delay={125}  // Frame when message appears (30fps)
/>

// Outgoing message (from user)
<Message
  text="Your outgoing message"
  isOutgoing={true}
  time="8:41 AM"
  delay={200}
  showCheck={true}
/>

// Typing indicator (shows "..." bubbles)
<TypingIndicator delay={80} duration={45} />
```

### 2. Timing Guide

- **30 fps** = 30 frames per second
- `delay={30}` = appears at 1 second
- `delay={60}` = appears at 2 seconds
- `duration={45}` = lasts 1.5 seconds

**Typical flow:**
1. First message: `delay={20}` (~0.7s)
2. Typing indicator: `delay={80}`, `duration={45}`
3. Response: `delay={125}` (after typing ends)
4. Next typing: `delay={175}`, `duration={45}`
5. Next response: `delay={220}`

### 3. Adjust Scrolling

In `ChatMessages`, update the scroll interpolation based on your message count:

```tsx
const scrollAmount = interpolate(
  frame,
  [scrollStart, scrollStart + 60, messageFrame, lastFrame],
  [0, firstScroll, firstScroll, finalScroll],
  { extrapolateLeft: "clamp", extrapolateRight: "clamp" }
);
```

Increase scroll values if messages overflow.

### 4. Text Formatting

Messages support:
- **Bold**: `**bold text**`
- `Code`: backticks around text
- Line breaks: `\n` in the string
- Emojis: just use them directly 🎬

### 5. Customizing the Header

In `ChatHeader` component, change:
- Name: `Pokey 🐡` → your assistant name
- Status: `online`
- Avatar emoji

### 6. Update Duration

In `Root.tsx`, set `durationInFrames` to match your video length:
- Count frames until last message appears + ~100 frames buffer
- At 30fps: 450 frames = 15 seconds

### 7. Render

```bash
# Standard render
npx remotion render WhatsAppDemo out/video.mp4 --concurrency=4

# Higher quality
npx remotion render WhatsAppDemo out/video.mp4 --codec h264 --crf 18

# Preview in browser
npm run dev
```

## Platform Dimensions

Edit `Root.tsx` to change dimensions:

| Platform | Dimensions | Aspect Ratio | Use Case |
|----------|------------|--------------|----------|
| **X/Instagram feed** | 1080×1350 | 4:5 | Default, most visible |
| **X/TikTok/Reels** | 1080×1920 | 9:16 | Full vertical |
| **X square** | 1080×1080 | 1:1 | Universal |
| **YouTube/X landscape** | 1920×1080 | 16:9 | Horizontal |

## Project Structure

```
~/Projects/remotion-test/
├── src/
│   ├── WhatsAppVideo.tsx   # Main video component
│   └── Root.tsx            # Composition config
├── public/
│   └── sounds/
│       ├── pop.mp3         # Message received
│       └── send.mp3        # Message sent
└── out/                    # Rendered videos
```

## Sound Effects

Sounds are triggered with Sequence:
```tsx
<Sequence from={125}>
  <Audio src={staticFile("sounds/pop.mp3")} volume={0.5} />
</Sequence>
```

## Tips

1. **Preview while editing**: Run `npm run dev` to see changes live
2. **Frame-by-frame**: Use timeline scrubber to check timing
3. **Keep messages concise**: Long messages may need scroll adjustment
4. **Test on mobile**: Check readability at actual size

## Asking Pokey to Generate

Just describe the conversation:
- "WhatsApp video: me asking you to [X]"
- "Make a chat video showing [conversation]"

Pokey will write the messages, set timing, render, and send the MP4.

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
