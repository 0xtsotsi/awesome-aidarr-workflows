# shitty-email

> Converted from OpenClaw Skill
> Original: [https://github.com/openclaw/skills/tree/main/skills/johanski/shitty-email/SKILL.md](https://github.com/openclaw/skills/tree/main/skills/johanski/shitty-email/SKILL.md)
> Category: Communication

---

## Description

Create and manage temporary disposable email inboxes

**Homepage:** N/A
**Repository:** N/A
**Version:** N/A

**Tags:** 

---

## GOTCHA Framework

### G - Goals
Create and manage temporary disposable email inboxes

### O - Orchestration
**Trigger:** User-invocable (via `aidarr run shitty-email`)
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
You are executing the shitty-email workflow. Use the following context:

Description: Create and manage temporary disposable email inboxes

Available tools: memory, http, context

Execute the workflow according to the user's request, leveraging ATLAS memory for persistence.
```

### A - Args

```yaml
name: shitty-email
category: Communication
version: 1.0.0
user_invocable: True
homepage: 
```

---

## Original Skill Content



# Shitty Email - Temporary Inbox Skill

Create disposable email addresses instantly. Perfect for signups, testing, and privacy.

## When to Use This Skill

Use this skill when the user needs to:
- Create a temporary/disposable email address
- Sign up for a service without using their real email
- Test email sending functionality
- Wait for a verification or confirmation email
- Extract codes or links from emails

## Important: Token Management

When you create an inbox, you receive a **token**. This token is required for ALL subsequent operations. Always store and reuse the token for the same inbox session.

## API Reference

Base URL: `https://shitty.email`

### Create a New Inbox

```bash
curl -s -X POST https://shitty.email/api/inbox | jq
```

Response:
```json
{
  "email": "abc1234@shitty.email",
  "token": "a1b2c3d4e5f6..."
}
```

**Store both the email and token** - you need the token for all other operations.

### Check Inbox for Emails

```bash
curl -s -H "X-Session-Token: {token}" https://shitty.email/api/inbox | jq
```

Response:
```json
{
  "emails": [
    {
      "id": "msg_a1b2c3d4e5",
      "from": "sender@example.com",
      "subject": "Welcome!",
      "date": "2026-02-03T12:00:00Z"
    }
  ]
}
```

### Get Full Email Content

Use the `id` field from the inbox response (e.g. `msg_a1b2c3d4e5`). This is NOT the email address.

```bash
curl -s -H "X-Session-Token: {token}" https://shitty.email/api/email/{email_id} | jq
```

Response includes `html` and `text` fields with the email body.

### Extend Inbox Lifetime

Inboxes expire after 1 hour by default. Extend by 1 hour (max 24 hours total):

```bash
curl -s -X POST -H "X-Session-Token: {token}" https://shitty.email/api/inbox/extend | jq
```

### Delete Inbox

Clean up when done:

```bash
curl -s -X DELETE -H "X-Session-Token: {token}" https://shitty.email/api/inbox
```

## Common Workflows

### Wait for a Verification Email

Poll the inbox until an email matching criteria arrives:

```bash
# Create inbox
RESPONSE=$(curl -s -X POST https://shitty.email/api/inbox)
EMAIL=$(echo $RESPONSE | jq -r '.email')
{token}=$(echo $RESPONSE | jq -r '.token')

# Poll for emails (check every 5 seconds, max 60 seconds)
for i in {1..12}; do
  EMAILS=$(curl -s -H "X-Session-Token: ${token}" https://shitty.email/api/inbox)
  COUNT=$(echo $EMAILS | jq '.emails | length')
  if [ "$COUNT" -gt "0" ]; then
    echo "Email received!"
    echo $EMAILS | jq '.emails[0]'
    break
  fi
  sleep 5
done
```

### Extract Verification Code

After receiving an email, extract common verification patterns:

```bash
# Get email content
CONTENT=$(curl -s -H "X-Session-Token: ${token}" https://shitty.email/api/email/${email_id} | jq -r '.text')

# Common patterns to look for:
# - 6-digit codes: grep -oE '[0-9]{6}'
# - Verification links: grep -oE 'https?://[^ ]+verify[^ ]*'
```

## Best Practices

1. **Reuse tokens** - Don't create new inboxes unnecessarily
2. **Poll responsibly** - Wait 5 seconds between checks
3. **Clean up** - Delete inbox when done to free resources
4. **Extend if needed** - If waiting for slow emails, extend the inbox

## Limitations

- Inboxes expire after 1 hour (extendable to 24 hours max)
- Email size limit: 1MB
- Rate limited: Don't spam inbox creation
- No outbound email - receive only

## Example Conversation

User: "Create a temp email for me"
→ Call POST /api/inbox, return the email address, store the token

User: "Sign me up for newsletter.example.com"
→ Use the temp email to fill the signup form, then poll for confirmation

User: "Did I get the confirmation?"
→ Check inbox using stored token, report results

User: "What's the verification code?"
→ Fetch email content, extract the code pattern, return it

User: "I'm done, delete the inbox"
→ Call DELETE /api/inbox with the token

---

*Converted by AiDarr Workflow Converter*
*Date: 2026-02-11*
