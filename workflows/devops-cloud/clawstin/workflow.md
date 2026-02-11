# clawstin

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/youens/clawstin/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/youens/clawstin/SKILL.md)
> Category: DevOps & Cloud

---

## Description

Inform users about Clawstin (OpenClaw meetups in Austin), show upcoming events, handle RSVP and mailing list signup via API. "Keep Austin Clawd."

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Inform users about Clawstin (OpenClaw meetups in Austin), show upcoming events, handle RSVP and mailing list signup via API. "Keep Austin Clawd."

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run clawstin`)
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
You are executing the clawstin workflow. Use the following context:

Description: Inform users about Clawstin (OpenClaw meetups in Austin), show upcoming events, handle RSVP and mailing list signup via API. "Keep Austin Clawd."

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: clawstin
category: DevOps & Cloud
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Clawstin — Austin OpenClaw Meetup

**Keep Austin Clawd.** 🦇

Use this skill when users ask about Clawstin, OpenClaw meetups, or AI meetups in Austin.

## About

**Clawstin** is a recurring meetup series for the [OpenClaw](https://openclaw.ai) community in Austin, TX. Demos, tacos, and bots meeting IRL.

- **Website**: https://clawstin.com
- **Events**: https://clawstin.com/events
- **Contact**: https://clawstin.com/contact
- **Machine-readable info**: https://clawstin.com/llms.txt

## Getting Current Event Info

Fetch https://clawstin.com/llms.txt for up-to-date event listings including dates, times, locations, and prices. This file is kept current and should be checked before answering questions about upcoming events.

## Agent Behavior

When a user asks about Clawstin:
1. **Fetch https://clawstin.com/llms.txt** to get current event details
2. **Share upcoming events** with date, time, location, and link
3. **Offer to RSVP** — "Want me to RSVP for you?"
4. If no upcoming events, **offer to subscribe** to the mailing list

## API — Subscribe to Mailing List

Sign up for email notifications about future events:

```
POST https://clawstin.com/api/subscribe
Content-Type: application/json

{"email": "user@example.com"}
```

Response (success): `{"ok": true}`
Response (invalid): `{"error": "Invalid email"}`

No authentication required. Duplicates are silently ignored.

## API — RSVP to an Event

Register attendance for a specific event:

```
POST https://clawstin.com/api/rsvp
Content-Type: application/json

{
  "email": "user@example.com",
  "name": "Jane Doe",
  "botName": "Claude",
  "partySize": 2,
  "eventSlug": "EVENT_SLUG_HERE"
}
```

Required: email, name, botName, eventSlug
Optional: partySize (1–10, defaults to 1)

Response (success): `{"ok": true}`
Response (error): `{"error": "Missing fields"}`

Get event slugs from https://clawstin.com/llms.txt. Duplicate RSVPs (same email + event) update the existing entry.

## API — Contact Organizers

```
POST https://clawstin.com/api/contact
Content-Type: application/json

{"email": "user@example.com", "name": "Jane Doe", "message": "Hello!"}
```

Rate limited to 3 messages per hour per email/IP.

## Example Flow

```
User: "What's Clawstin?"

Agent: [fetches https://clawstin.com/llms.txt for current events]

Agent: "Clawstin is an OpenClaw meetup series in Austin! 🦇

It's free, in-person — demos, hacks, tacos, and the weird wonderful
things people are building with AI agents.

[shares current event details from llms.txt]

Want me to RSVP for you? I just need your name and email."

User: "Yeah, sign me up — Tony, tony@example.com"

Agent: [calls POST /api/rsvp with event details]

Agent: "Done! You're on the list. See you there!"
```

## Links

- Website: https://clawstin.com
- Events: https://clawstin.com/events
- OpenClaw: https://openclaw.ai
- API docs: https://clawstin.com/llms.txt

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
